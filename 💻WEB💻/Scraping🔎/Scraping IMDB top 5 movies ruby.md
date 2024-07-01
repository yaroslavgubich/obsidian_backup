require "open-uri"
require "nokogiri"

def fetch_movie_urls
  top_url = "https://www.imdb.com/chart/top"
  html_file = URI.open("https://www.imdb.com/chart/top/", "Accept-Language" => "en-US", "User-Agent" => "Mozilla/5.0 (Linux; Android 6.0.1; Nexus 5X Build/MMB29P) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/W.X.Y.Z Mobile Safari/537.36 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)").read
  doc = Nokogiri::HTML.parse(html_file)
  movies = doc.search(".ipc-title-link-wrapper")
  movies.take(5).map do |movie|
    suffix = movie.attributes["href"].value
    "https://www.imdb.com#{suffix}"
  end
end

def scrape_movie(url)
  ## open and read the URL
  html_file = URI.open(url, "Accept-Language" => "en-US", "User-Agent" => "Mozilla/5.0 (Linux; Android 6.0.1; Nexus 5X Build/MMB29P) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/W.X.Y.Z Mobile Safari/537.36 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)").read
  doc = Nokogiri::HTML.parse(html_file)
  # hero__primary-text
  title = doc.search("h1").text
  year = doc.xpath("//*[@id='__next']/main/div/section[1]/section/div[3]/section/section/div[2]/div[1]/ul/li[1]/a").text.to_i
  storyline = doc.xpath("//*[@id='__next']/main/div/section[1]/section/div[3]/section/section/div[3]/div[2]/div[1]/section/p/span[1]").text
  cast = doc.xpath("//a[@data-testid='title-cast-item__actor']").map { |element| element.text }.first(3)
  director = doc.xpath("//*[@id='__next']/main/div/section[1]/div/section/div/div[1]/section[4]/ul/li[1]/div").text

  {
    title: title,
    cast: cast,
    director: director,
    storyline: storyline,
    year: year
  }
end
