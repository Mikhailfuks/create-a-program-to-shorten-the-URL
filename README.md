const shortener = document.getElementById('shortener');
const result = document.getElementById('result');
const copyButton = document.getElementById('copyButton');

// Функция генерации короткого URL
function generateShortURL(longURL) {
  // Простая реализация: используется случайная строка
  const shortCode = Math.random().toString(36).substring(2, 10);
  return `${window.location.origin}/short/${shortCode}`; // Возвращаем полный короткий URL
}

// Обработка отправки формы
shortener.addEventListener('submit', (event) => {
  event.preventDefault();
  const longURL = document.getElementById('longURL').value;

  if (longURL) {
    const shortURL = generateShortURL(longURL);
    result.textContent = shortURL;
    result.style.display = 'block';
    copyButton.style.display = 'block';
  } else {
    alert('Введите полный URL.');
  }
});

// Функция копирования в буфер обмена
copyButton.addEventListener('click', () => {
  navigator.clipboard.writeText(result.textContent)
    .then(() => {
      alert('Короткий URL скопирован!');
    })
    .catch(err => {
      console.error('Failed to copy: ', err);
    });
});

<!DOCTYPE html>
<html>
<head>
  <title>Сократитель URL</title>
</head>
<body>
  <form id="shortener">
    <label for="longURL">Полный URL:</label>
    <input type="text" id="longURL" placeholder="https://www.example.com" required>
    <button type="submit">Сократить</button>
  </form>
  <div id="result" style="display: none;">
    <p>Короткий URL: <span id="shortURL"></span></p>
    <button id="copyButton" style="display: none;">Копировать</button>
  </div>
  <script src="script.js"></script>
</body>
</html>

