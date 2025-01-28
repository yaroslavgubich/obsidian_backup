require_relative "../scraper"

describe "#fetch_movie_urls" do
  it "returns an array of movies" do
    actual = fetch_movie_urls
    expected = [
      "https://www.imdb.com/title/tt0111161/?ref_=chttp_t_1",
			"https://www.imdb.com/title/tt0068646/?ref_=chttp_t_2",
      "https://www.imdb.com/title/tt0468569/?ref_=chttp_t_3",
      "https://www.imdb.com/title/tt0071562/?ref_=chttp_t_4",
      "https://www.imdb.com/title/tt0050083/?ref_=chttp_t_5"
    ]
    expect(actual).to eq(expected)
  end
end

describe "#scrape_movie" do
  it "returns a Hash describing a movie" do
    batman_url = "https://www.imdb.com/title/tt0468569/?ref_=chttp_t_3"
    movie_details = scrape_movie(batman_url)

    expected = {
      cast: [ "Christian Bale", "Heath Ledger", "Aaron Eckhart" ],
      director: "Christopher Nolan",
      storyline: "When the menace known as the Joker wreaks havoc and chaos on the people of Gotham, Batman must accept one of the greatest psychological and physical tests of his ability to fight injustice.",
      title: "The Dark Knight",
      year: 2008
    }
    expect(movie_details).to eq(expected)
  end
end

