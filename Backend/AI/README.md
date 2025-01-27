# Backend Documentation

Base URL: http://52.163.230.167:5000
## Start Server
### 1. With Docker 
```bash
cd ~
cd viBlind/Backend/AI/
docker-compose up
```
### 2. Without Docker
```bash
cd ~
cd viBlind/Backend/AI/
virtualenv -p python3 venv
source venv/bin/activate
pip3 install -r requirements.txt
sudo chmod +x run.sh
./run.sh
```

## API References

| HTTP Method |            Resource URL            |                                Notes                               |  Data Type |
|:-----------:|:----------------------------------:|:------------------------------------------------------------------:|:----------:|
|  POST, GET  |           /v1/api/predict          | Send an image want to recognize, return objects recognition texts  |    JSON    |
|POST, GET|/v1/api/summarize|Send an article want to summarize, return a summarized article |TEXT|
|POST, GET|/v1/api/answer_question|Send a question related to a specific article, return answers for that question|JSON

### Examples
Assume we have an ```dog-and-cat.png``` in local.

__1.__ _/v1/api/predict_ (POST, GET)

__Request:__ 
```js
Header = {
    "content-type": "application/json"
}

Body = {
    "image" : "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAIBAQEBAQIBAQECAg..."   // Encode image as base64 
    "name" :  "dog-and-cat.png"
}
```
__Response:__

```js
{
  "objectProperty": [{
    "text": "dog",
    "confidence": 0.8863365650177002,
    //"color": "red",
    "x": 840,        // (x, y) is the coordinates of the upper-left corner of the bounding box
    "y": 75,
    "width": 1236,   //  (width, height) is the bouding box size
    "height": 615
  }, {
    "text": "cat",
    "confidence": 0.8379455804824829,
    //"color": "red",
    "x": 47,        // (x, y) is the coordinates of the upper-left corner of the bounding box
    "y": 54,
    "width": 1004,  //  (width, height) is the bouding box size
    "height": 650 
  }]
}
```
__2.__ _/v1/api/summarize_ (POST, GET)

__Request:__ 
```js
Header = {
    "content-type": "application/json"
}

Body = {
    "articleContent": "South Park, one of Seattle’s dwindling blue-collar pockets, is on the rise. Yet the scruffy, geographically isolated enclave has managed to transform itself without losing its soul to gentrification, causing outsiders — including other Seattleites — to take notice.Situated on the western shore of the Duwamish River in a hard-to-reach corner of the city, South Park has turned its relative remoteness and affordability into an advantage, attracting creative entrepreneurs who otherwise might not be able to set up shop in one of the nation’s fastest growing cities. (Rents are cheaper here.)A hip wine shop, a brewery and a handful of new restaurants and bars greet interlopers who cross the neighborhood’s main artery to mainland Seattle, the South Park Bridge.Home to several Boeing operations and a slew of fabricators and machine shops, the heavily industrial neighborhood was considered one of Seattle’s grittier areas for decades — when it was even considered at all. Things began to percolate a bit about a decade ago with the opening of  Loretta’s Northwesterner, a tavern known for its burgers, but suffered a setback when the South Park Bridge was closed for a four-year repair.Now, though, with the bridge’s reopening in 2014, South Park has seen a revitalization that has not yet brought on full-bore gentrification. Industry remains prominent in the area, protected by zoning and geographic forces, including being hemmed in by the river and a phalanx of highways.“Perhaps the upside of being located farther afield is that a close-knit community’s been formed that’s flown relatively under the radar — and thus been less susceptible — to gentrifying forces,” said Cynthia Brothers, the founder of Vanishing Seattle, her one-woman organization that documents endangered small businesses and cultural institutions on Instagram and other mediums.Sharing that view is Coté Soerens, a Chilean immigrant, who in 2018 opened Resistencia Coffee with her husband, Tim, in the heart of the neighborhood where they live with  their two young sons.“If everything is too polished and finished, it’s super boring,” Ms. Soerens said. South Park also appealed to Dan Slemko, who moved to the neighborhood in 1997. The 60-year-old former Boeing employee owns a waterfront home on the Duwamish River, which sounds sexier than it is. Seattle is a city known for its pristine waterways, but the Duwamish was so polluted that it was declared a Superfund site in 2001. It’s a working river in a working-class neighborhood. It’s slowly getting cleaner, as is South Park.Shortly after Mr. Slemko got his last box unpacked, he drove to the now-defunct County Line, a raucous saloon near the South Park Bridge, and promptly got his headlights smashed out.Many neighborhoods would perhaps enlist law enforcement to deal with such an establishment. But not South Park: According to Loretta’s owner Scott Horrell, a group of residents instead designated a night to drink together at The County Line — to meet the rabble rousers on their own turf rather than calling the authorities.Such is the welcoming spirit of South Park in a city that in recent years has been dynamically changed by population growth, with many newcomers reshaping Seattle.When the bridge closed in 2010, South Park became even more choked off from the rest of the city (there are alternative access points, but they’re few and mostly intricate), which had an effect that surprised and encouraged Mr. Horrell.“The bridge closure was terrifying, but it turned us into an island. It solidified us and our regulars. They were trapped,” said Mr. Horrell, a physically imposing former trucker who became South Park’s foremost beer and burger proprietor — as well as a resident.Since the bridge reopened in 2014 — and especially since new restaurants and watering holes  opened near South Park’s main intersection of 14th Ave. S. and S. Cloverdale St.— Seattleites are increasingly seeking South Park out. And because of skyrocketing housing costs in Seattle, younger residents are increasingly buying homes in South Park, a genuinely diverse neighborhood with a lush community garden called Marra Farm.Campbell Scarborough and his wife, Katie Escudero, moved to Seattle from Los Angeles, and bought a modern home in South Park four years ago. South Park reminds Ms. Escudero of Los Angeles’s Echo Park neighborhood, while Mr. Scarborough considered it a “no-brainer” in 2017 to open Left Bank, South Park’s oldest wine shop — because it’s the only one — at the intersection of 14th and Cloverdale.The couple sells modestly priced European wines out of a space so small that “you can’t really come here and have an intimate conversation,” Mr. Scarborough explained. Patrons bring their own vinyl albums to spin on the shop’s stereo on Tuesdays, and the owners keep Rainier beer on tap just so Mr. Slemko, a cheap-beer aficionado known to locals as “River Dan,” feels right at home when he swings by each night.Mr. Slemko is well known for his parties. His Fourth of July bash — replete with fireworks and live music — reportedly rivals the region’s officially sanctioned celebrations.“I’ve been to enough of his parties to be immune to the noise. And if you don’t like it, it’ll be over in a few hours,” said Dave Wilkinson, who owns a house down the street from Mr. Slemko’s.Central to South Park’s transformation has been Mr. Horrell’s business partner, John Bennett, who has developed a knack for scooping up old buildings in hardscrabble neighborhoods like South Park and nearby Georgetown, and subsequently resisting the urge to replace them with shiny new condominiums.One of Mr. Bennett’s tenants at 14th and Cloverdale, Corina Luckenbach, operates a former ballroom and billiards parlor called South Park Hall, which is now a multiuse space that has everything from square-dance potlucks and Jazzercise classes to karaoke brunches.Ms. Luckenbach said Mr. Bennett’s ethos is to “rent to people who are struggling to pay the rent.”Risk-taking and an all-in mentality ensue. “Most of the people I know who open these places use every dime they have,” said Mr. Horrell, who counts himself among that flock.In June 2017, Ms. Soerens and her husband, Tim, nearly died in an automobile accident after getting struck by a drunken driver in Mexico while celebrating their 10th wedding anniversary. One year later, they opened their coffee shop, Resistencia, near the intersection of 14th and Cloverdale, and business has been brisk.The Soerenses live near the community garden, Marra Farm, and positioned a pair of hospital beds in their living room during their recovery from the crash. For three months, Ms. Soerens said neighbors brought meals, cared for the couple’s sons, walked their dog, and otherwise caught up with one another.It was immensely helpful, exhausting and exhilarating — and served to cement the couple’s commitment to their tight-knit community.52 PLACES AND MUCH, MUCH MORE Follow our 52 Places traveler, Sebastian Modak, on Instagram as he travels the world, and discover more Travel coverage by following us on Twitter and Facebook. And sign up for our Travel Dispatch newsletter: Each week you’ll receive tips on traveling smarter, stories on hot destinations and access to photos from all over the world."
}
```
__Response:__

```js
{
    "(Rents are cheaper here.)A hip wine shop, a brewery and a handful of new restaurants and bars greet interlopers who cross the neighborhood\\u2019s main artery to mainland Seattle, the South Park Bridge.Home to several Boeing operations and a slew of fabricators and machine shops, the heavily industrial neighborhood was considered one of Seattle\\u2019s grittier areas for decades \\u2014 when it was even considered at all.\\nIndustry remains prominent in the area, protected by zoning and geographic forces, including being hemmed in by the river and a phalanx of highways.\\u201cPerhaps the upside of being located farther afield is that a close-knit community\\u2019s been formed that\\u2019s flown relatively under the radar \\u2014 and thus been less susceptible \\u2014 to gentrifying forces,\\u201d said Cynthia Brothers, the founder of Vanishing Seattle, her one-woman organization that documents endangered small businesses and cultural institutions on Instagram and other mediums.Sharing that view is Cot\\u00e9 Soerens, a Chilean immigrant, who in 2018 opened Resistencia Coffee with her husband, Tim, in the heart of the neighborhood where they live with  their two young sons.\\u201cIf everything is too polished and finished, it\\u2019s super boring,\\u201d Ms. Soerens said.\\nAnd because of skyrocketing housing costs in Seattle, younger residents are increasingly buying homes in South Park, a genuinely diverse neighborhood with a lush community garden called Marra Farm.Campbell Scarborough and his wife, Katie Escudero, moved to Seattle from Los Angeles, and bought a modern home in South Park four years ago.\\nAnd if you don\\u2019t like it, it\\u2019ll be over in a few hours,\\u201d said Dave Wilkinson, who owns a house down the street from Mr. Slemko\\u2019s.Central to South Park\\u2019s transformation has been Mr. Horrell\\u2019s business partner, John Bennett, who has developed a knack for scooping up old buildings in hardscrabble neighborhoods like South Park and nearby Georgetown, and subsequently resisting the urge to replace them with shiny new condominiums.One of Mr. Bennett\\u2019s tenants at 14th and Cloverdale, Corina Luckenbach, operates a former ballroom and billiards parlor called South Park Hall, which is now a multiuse space that has everything from square-dance potlucks and Jazzercise classes to karaoke brunches.Ms. Luckenbach said Mr. Bennett\\u2019s ethos is to \\u201crent to people who are struggling to pay the rent.\\u201dRisk-taking and an all-in mentality ensue."    
}   // article's content which has been summarized
```

__3.__ _/v1/api/answer_question_ (POST, GET)

__Request:__ 
```js
Header = {
    "content-type": "application/json"
}

Body = {
    "question": "What did the sailor do?",
    "hash_url": "C5B5300ECED62665ACC6CA32A0BEB39AE942B861"
}
```
__Response:__

```js
{
    'answers':
        [
            {
                'result':'',    // result with highest capacity
                'score':''      // score of the result
            }, 
            {
                'result':'',    // second
                'score':''
            }, 
            {
                'result':'',    // third
                 'score':''
             }
        ]
}
```
