---
clock_in: {{date:YYYY-MM-DD HH:mm:ss}}
clock_out: 
---
### [[<% tp.date.now("YYYY-MM-DD", -1, tp.file.title, "YYYY-MM-DD") %>| <<]] | **Today is Accidentally Awesome!** | [[<% tp.date.now("YYYY-MM-DD", 1, tp.file.title, "YYYY-MM-DD") %> | >> ]]

### 📚 밀린 거
```tasks
not done 
path does not include {{query.file.path}}
path regex matches /TODO/
id does not include 25
sort by due, scheduled
```

#### 🤦‍♂️ 개쩌는 인턴 생활
- [x] [[GraphCast Butterfly Effect Test#Procedure]] 진행상황 업데이트 ✅ 2024-09-30
<%*
let date = moment(tp.file.title, "YYYY-MM-DD");
let dayOfWeek = date.day();
%>
#### 👨‍🏫 개쩌는 조교 생활
<%* if (dayOfWeek == 1) { %>
- [x] 현대시 읽기 채점하기 ✅ 2024-09-30
- [x] 한국현대시인론 채점하기 ✅ 2024-09-30
- [x] 이수정 교수님께 메일 쏘기 | <% date %> ✅ 2024-09-30
<%* } %>
<%* if (dayOfWeek == 5) {%>
- [x] 그래프이론 오피스아워 오픈오픈👩‍💻👨‍💻 ✅ 2024-09-30
<%*}%>

#### 🏭 생산적으로 살기

#### 🍻 Relax & Chill 
<%*
// 평일
if (dayOfWeek >= 1 && dayOfWeek <= 5) {
  tR += "- [ ] CROSSFIT 죠지기🏋️‍♀️ | 🆔 25\n";
}

// 금요일
if (dayOfWeek == 5) {
  //tR += "- [ ] 힙합 죠져~🤸‍♂️ | 🆔 25\n";
}

// 일요일
if (dayOfWeek === 0) {
  //tR += "- [ ] 힙합 죠져~🤸‍♂️ | 🆔 25\n";
}
%>

#### 💨뒤.로.미.루.기

#### 🌪 생각이 돌아가는 중