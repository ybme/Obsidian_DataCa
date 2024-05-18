#### 入职时间：2018/07/11
#### 离职时间：2023/05/18

```dataviewjs
// 获取当前文件内容
const content = dv.io.load(dv.current().file.path);
content.then(documentContent => {
    // 使用正则表达式提取入职时间和离职时间，支持 yyyy/mm/dd 和 yyyy-mm-dd 格式
    const joinDateRegex = /入职时间：(\d{4}[-\/]\d{1,2}[-\/]\d{1,2})/;
    const leaveDateRegex = /离职时间：(\d{4}[-\/]\d{1,2}[-\/]\d{1,2})/;

    const joinDateMatch = documentContent.match(joinDateRegex);
    const leaveDateMatch = documentContent.match(leaveDateRegex);

    if (joinDateMatch) {
        const specifiedJoinDate = new Date(joinDateMatch[1].replace(/-/g, '/')); // 提取到的入职时间
        const specifiedLeaveDate = leaveDateMatch ? new Date(leaveDateMatch[1].replace(/-/g, '/')) : new Date(); // 提取到的离职时间或当前时间

        const timeDifference = specifiedLeaveDate - specifiedJoinDate;

        // 计算年、月、天的差异
        const yearsDifference = specifiedLeaveDate.getFullYear() - specifiedJoinDate.getFullYear();
        const monthsDifference = specifiedLeaveDate.getMonth() - specifiedJoinDate.getMonth();
        const daysDifference = specifiedLeaveDate.getDate() - specifiedJoinDate.getDate();

        // 调整月份和天数
        let adjustedYears = yearsDifference;
        let adjustedMonths = monthsDifference;
        let adjustedDays = daysDifference;

        if (adjustedDays < 0) {
            adjustedMonths -= 1;
            const previousMonth = new Date(specifiedLeaveDate.getFullYear(), specifiedLeaveDate.getMonth(), 0);
            adjustedDays += previousMonth.getDate();
        }

        if (adjustedMonths < 0) {
            adjustedYears -= 1;
            adjustedMonths += 12;
        }

        // 计算总天数
        const totalDays = Math.floor(timeDifference / (1000 * 3600 * 24)); // 将时间差转换为天数

        dv.paragraph(`###### 入职时间： ${specifiedJoinDate.toISOString().split('T')[0]}${leaveDateMatch ? ` ，离职时间： ${specifiedLeaveDate.toISOString().split('T')[0]}` : ''} ，工龄： ${adjustedYears} 年 ${adjustedMonths} 月 ${adjustedDays} 天 (${totalDays} 天)`);
    } else {
        dv.paragraph("未找到有效的入职时间。请检查文档格式。");
    }
});
```
