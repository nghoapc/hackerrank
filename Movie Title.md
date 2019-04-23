# Problem:
### To solve this challenge, you are required to write an HTTP GET method to retrieve information from a movie database.   Function Description Given a string substr, getMovieTitles must perform the following tasks: Query https://jsonmock.hackerrank.com/api/movies/search/?Title=substr(replace substr).  Initialize the titles array to store total string elements. Store the Title of each movie meeting the search criterion in the titles array. Sort titles in ascending order and return it as your answer.   The query response from the website is a JSON response with the following five fields: page: The current page. per_page: The maximum number of results per page. total: The total number of movies in the search result. total_pages: The total number of pages which must be queried to get all the results. data: An array of JSON objects containing movie information where the Title field denotes the title of the movie.   In order to get all results, you may have to make multiple page requests. To request a page by number, your query should read https://jsonmock.hackerrank.com/api/movies/search/?Title=substr&page=pageNumber, replacing substr and pageNumber.

```sh
#!/bin/ruby

require 'net/http'
require 'json'


# Complete the function below.
# Base url: https://jsonmock.hackerrank.com/api/movies/search/?Title=
require 'json'
require 'open-uri'

def getMovieTitles(substr) 
  page_num = 1
  url = 'https://jsonmock.hackerrank.com/api/movies/search/?Title=' + substr + '&page=' + page_num.to_s
  res = open(url).read
  res = JSON.parse(res)
  movies = res['data']
  total_page = res['total_pages']
  array_sorted = []
  movies.each do |m|
   array_sorted << m['Title']
  end
  (2..total_page).each do |i|
    current_page = i
    url = 'https://jsonmock.hackerrank.com/api/movies/search/?Title=' + substr + '&page=' + current_page.to_s
    res = open(url).read
    res = JSON.parse(res)
    movies = res['data']
    movies.each do |m|
        array_sorted << m['Title']
    end
  end
  array_sorted.sort
end

fp = File.open(ENV['OUTPUT_PATH'], 'w')
    

_substr = gets.to_s.strip;

res = getMovieTitles(_substr);
for res_i in res do
  fp.write res_i
  fp.write "\n"
end

fp.close()
```