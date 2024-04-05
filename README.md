
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>캘린더</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<div id="calendar-container"></div>
<div id="memo-container" style="display: none;">
    <textarea id="memo-text"></textarea>
    <button onclick="saveMemo()">저장</button>
    <button onclick="cancelMemo()">취소</button>
</div>
<script>
const calendarContainer = document.getElementById('calendar-container');
const memoContainer = document.getElementById('memo-container');
const memoText = document.getElementById('memo-text');

let currentDate;

function renderCalendar(year, month) {
  const today = new Date(year, month, 1);
  const lastDay = new Date(year, month + 1, 0).getDate();
  
  let html = '<div class="calendar">';
  html += '<table>';
  html += '<tr><th colspan="7">' + today.toLocaleDateString('en-US', { month: 'long', year: 'numeric' }) + '</th></tr>';
  html += '<tr><th>Sun</th><th>Mon</th><th>Tue</th><th>Wed</th><th>Thu</th><th>Fri</th><th>Sat</th></tr>';
  
  let day = 1;
  for (let i = 0; i < 6; i++) {
    html += '<tr>';
    for (let j = 0; j < 7; j++) {
      if (i === 0 && j < today.getDay()) {
        html += '<td></td>';
      } else if (day > lastDay) {
        html += '<td></td>';
      } else {
        html += '<td onclick="showMemo(' + day + ')">' + day + '</td>';
        day++;
      }
    }
    html += '</tr>';
  }
  html += '</table>';
  html += '</div>';
  
  return html;
}

function showMemo(day) {
  currentDate = new Date(new Date().getFullYear(), new Date().getMonth(), day);
  memoText.value = localStorage.getItem(currentDate.toISOString()) || '';
  memoContainer.style.display = 'block';
}

function saveMemo() {
  localStorage.setItem(currentDate.toISOString(), memoText.value);
  memoContainer.style.display = 'none';
  renderCalendar(currentDate.getFullYear(), currentDate.getMonth());
}

function cancelMemo() {
  memoContainer.style.display = 'none';
}

// 현재 월을 기준으로 앞뒤 3개월씩 캘린더 생성
let today = new Date(2023, 5, 1);
let year = today.getFullYear();
let month = today.getMonth();
for (let i = -1; i <= 1; i++) {
  let calendarDiv = document.createElement('div');
  calendarDiv.classList.add('calendar');
  calendarDiv.innerHTML = renderCalendar(year, month + i);
  calendarContainer.appendChild(calendarDiv);
}
</script>
</body>
</html>
