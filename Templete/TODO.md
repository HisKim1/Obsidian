---
clock_in: {{date:YYYY-MM-DD HH:mm:ss}}
clock_out: 
---
### [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>| <<]] | **Today is Acctidentally Awesome!** | [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %> | >> ]]

### 📚 밀린 거
```tasks
not done 
due in or after {{date}} - path includes {{date}} 
sort by scheduled, due
```

#### 🤦‍♂️개쩌는 인턴 생활


#### 🍻 Relax & Chill 
<%*
let date = moment(tp.file.title, "YYYY-MM-DD");
let dayOfWeek = date.day();

// 평일
if (dayOfWeek >= 1 && dayOfWeek <= 5) {
  tR += "- [ ] CROSSFIT 조지기\n";
}

// 금요일
if (dayOfWeek == 5) {
  tR += "- [ ] 힙합 죠져~\n";
}

// 일요일
if (dayOfWeek === 0) {
  tR += "- [ ] 힙합 죠져~\n";
}
%>
### What to work on tomorrow?
`ctrl + L`
