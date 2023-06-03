import requests
from bs4 import BeautifulSoup 
import pprint
#Beautifulsoup -> use html and grab data 
#requests module -> download that initial htm;

response = requests.get('https://news.ycombinator.com/news') 
#get method to grab the page

#get html text/ requested page 
print(response.text)

#clean up data with beautifulsoup -> convert uncleaned text 
#doc or string to object that can be manipluated
#from html /string to parse it to object called soup object
soup = BeautifulSoup(response.text, 'html.parser')

# #bs also parses - xml data 
# #what is 'html.parser' ->default, 

print(soup) 
 print(soup.body)
 print(soup.body.contents)
get all divs in a list form
 print(soup.find_all('a'))
print(soup.title)
print(soup.find('a'))
selectively pick what data we want
print(soup.find(id ='score_20514755'))
#select allows us to grab data from the soup var downloaded & created \

# #using CSS SELECTOR -> ways to grab elements from a html doc
# # #get all the links
 print(soup.select('a'))

# #get classes from doc -> list of all the spans that has class of score (.)-stands for class
 print(soup.select('.score'))

# #get id from doc
 print(soup.select('#score_20514755'))

# #FILTERING -> get title & get votes > 100
print(soup.select('.titleline')) 
links = soup.select('.titleline')
 votes = soup.select('.score')
print(votes[0])
# #reuturns a list , to grab the first element
print(soup.select('.titleline')[0]) 
print(votes[0].get('id'))

response = requests.get('https://news.ycombinator.com/news?p=1') 
response2 = requests.get('https://news.ycombinator.com/news?p=2')
soup = BeautifulSoup(response.text, 'html.parser')
soup2 = BeautifulSoup(response2.text, 'html.parser')

#links for page 1
links = soup.select('.titleline > a')
 votes = soup.select('.score')
subtext = soup.select('.subtext')


#links for page 2
links2 = soup2.select('.titleline > a')
votes = soup.select('.score')
subtext2 = soup2.select('.subtext')

#merge two pages together
mega_links = links + links2
mega_subtext = subtext + subtext2

def sort_stories_by_votes(hnlist):
   #lambda expression for sorting dictionaries
   return sorted(hnlist, key = lambda k:k['votes'], reverse= True)

#FILTERING FOR LINKS AND TEXT(TITLE)
#def create_custom_hakernews(links,votes):
def create_custom_hakernews(links,subtext):
    hn = []
    for index,item in enumerate(links):
        
        title = links[index].getText()
        href = links[index].get('href')
        vote = subtext[index].select('.score')
        if len(vote):
          points = int(vote[0].getText().replace(' points',''))
          print(points)
          if points >100:
             hn.append({'title':title, 'link': href, 'votes': points})
    return sort_stories_by_votes(hn)
