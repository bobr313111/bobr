<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Simple Web Proxy</title>
<style>
  body { font-family: Arial, sans-serif; margin: 20px; background: #f0f0f0; }
  input, button { padding: 8px; font-size: 14px; margin: 5px; }
  iframe { width: 100%; height: 80vh; border: none; margin-top: 10px; }
</style>
</head>
<body>
<h2>Web Proxy for Chromebook</h2>
<input type="text" id="url" placeholder="https://example.com" size="50">
<button onclick="go()">Go</button>
<iframe id="frame"></iframe>

<script>
function go() {
    let url = document.getElementById('url').value;
    if (!url.startsWith('http')) url = 'https://' + url;

    // Используем бесплатный прокси-сервис
    const proxy = "https://api.allorigins.win/get?url=";
    const frame = document.getElementById('frame');

    // Загружаем страницу через прокси
    fetch(proxy + encodeURIComponent(url))
    .then(response => response.json())
    .then(data => {
        frame.srcdoc = data.contents;
    })
    .catch(err => alert("Ошибка: " + err));
}
</script>
</body>
</html>
