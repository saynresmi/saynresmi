document.addEventListener("DOMContentLoaded", function() {
    fetchNews();
});

// Haberleri çekmek ve sayfada göstermek
function fetchNews() {
    fetch(API_URL)
        .then(response => response.json())
        .then(data => {
            const newsContainer = document.getElementById('news-container');
            data.articles.forEach(news => {
                const newsCard = document.createElement('div');
                newsCard.classList.add('news-card');
                
                const newsTitle = document.createElement('h3');
                newsTitle.textContent = news.title;
                
                const newsDescription = document.createElement('p');
                newsDescription.textContent = news.description;

                const newsLink = document.createElement('a');
                newsLink.href = news.url;
                newsLink.textContent = "Devamını oku";
                newsLink.target = "_blank";  // Yeni sekmede açmak için

                // Haber kartını oluştur
                newsCard.appendChild(newsTitle);
                newsCard.appendChild(newsDescription);
                newsCard.appendChild(newsLink);

                // Haberi sayfada göster
                newsContainer.appendChild(newsCard);
            });
        })
        .catch(error => {
            console.error("Haberler alınamadı: ", error);
        });
}
