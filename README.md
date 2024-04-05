<
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>캘린더</title>
<link rel="stylesheet" href="styles.css">
</head>
<body>
<div id="calendar"></div>
<div id="memo-container" style="display: none;">
    <textarea id="memo-text"></textarea>
    <button onclick="saveMemo()">저장</button>
    <button onclick="cancelMemo()">취소</button>
</div>
<script src="script.js"></script>
</body>
</html>
