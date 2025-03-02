---
layout: post
title: "Regex Code-Through in R"
date: 2025-03-01
categories: [R, regex, data analytics]
---

Regular expressions (Regex) are a powerful tool for text manipulation and data cleaning, which are essential data analytics skills. In this code-through, we’ll dive into practical applications of Regex in R using real-world product review data.

## Introduction

This code-through will explore additional use cases of regular
expressions within R by using the Amazon Fine Food Reviews dataset from
Kaggle.

You can find the direct link here: [Kaggle
Dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews/data)

For a brief description of this dataset, it contains reviews of fine
foods from Amazon. The dataset contains product/user
information, ratings, and reviews.

## Learning Objectives

Our goal for this CodeThrough is to filter the reviews to answer a
couple of business questions, and also clean the datasets.

*Step 1: Load Amazon Review Dataset*

``` r
# As mentioned, please refer to the Kaggle link I provded above to download
# the dataset. It is quite a big file, so it may take some time!

# Define file path
dataset_path <- "/Users/kalanicook/Downloads/amazon_kaggle/Reviews.csv"

# Load the dataset in R
reviews <- read_csv(dataset_path)

# View the first few rows
head(reviews)
```

<br>

*Step 2: Filter Reviews with RegEx*

For our first scenario, we want to filter the reviews that mention key
terms such as “Refund” or “Money”. This could give us an idea of
customer complaints.

<br>

``` r
refund_reviews <- reviews %>%
  filter(str_detect(Text, "(?i)refund|money back|return"))

head(refund_reviews$Text, 5)
```

    ## [1] "This wasn't in stock the last time I looked. I had to go to the Vermont Country Store in Weston to find it along with a jaw harp, Cranberry Horseradish Sauce, Fartless Black Bean Salsa, Apple Cider Jelly, Newton's Cradle Art in Motion and the staple Vermont Maple Syrup.<br /><br />Back to the Ass Kickin Peanuts. They are hot. They will activate the perspiration glands behind your ears and under your arms. It requires a beverage as advertised, a glass of very cold milk, and a box of Kleenex since it will make your nose run. They look like ordinary peanuts which is already giving me ideas for work. I suspect that some people have been hitting my goodies in my absence, especially my colleague Greg. I'm going to take this to work at earliest opportunity and empty the contents of this can into an ordinary Planters Peanuts can, and then see whose crying or whose nose is running when I return.<br /><br />The can should be shaken to ensure the spices are evenly distributed. It is important to wash your hands after consumption and not touch the eyes.<br /><br />You'll go nuts over these Ass-Kickin' Peanuts.<br /><br />P.S. I'm not sharing the peanuts, not deliberately, and I'll probably give Greg the jaw harp for Christmas. He'll be so insulted."
    ## [2] "No tea flavor at all. Just whole brunch of artifial flavors. It is not returnable. I wasted 20+ bucks."                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  
    ## [3] "Arrived slightly thawed. My parents wouldn't accept it. However, the company was very helpful and issued a full refund."                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 
    ## [4] "The SALSA smelled delicious, as I think it probably was - but, unfortunately, the person, at AMAZON, that is a packer (there is probably several) had very little \"stuffing\" to work with, especially on the bottoms.  Therefore, the bottoms were broken on all three bottles. As I reached for my computer; I was told NO RETURNS (cause it's a food item).  I then looked for a CUSTOMER SERVICE tag; and I found \"none\" on their NEW FACE LIFT.  THEY SEEM TO BE PROUD OF THEIR NEW FACE LIFT BUT...THEY SHOULD AT LEAST HAVE A PLACE TO CONTACT THEM IN EMERGENCIES!  LIKE: I BUY A LOT OF \"STUFF\" AND IT ALL COMES IN STYROFOAM BOXES.  NEVER WOULD I SHIP THINGS<br />ESPECIALLY SALSA - IN A CARDBOARD BOX WITH JUST A STRIPE OF LARGE BUBBLE WRAP ON IT.  NO MATTER HOW MUCH THE CARRIER (FED EX) IS CAREFUL, IT'S GOING TO BREAK SOMEWHERE ALONG THE LINE.  ESPECIALLY IN AN ALL GLASS CONTAINER!  BARBARA L. S."                                                                                                                                                                                                                                                                                                                                                                        
    ## [5] "I don't know how long these sat on the back of a shelf somewhere, but they were so old that they wouldn't cook.  I had to throw half of them out, because the skins were damaged, a clear sign of dried beans past their prime.  I can't even return these or ask for a refund, because food is not returnable.  Will find a different brand to use.  For now, I have about fifty servings of beans to throw away."

<br>

Logic: By using str_detect(), the function works to search through our
Reviews.csv file and return reviews that match the requested pattern.

(?i) - is used to make the search case insenstive.

<br>

Following this, let’s do the opposite and filter for reviews that are
positive.

<br>

``` r
positive_reviews <- reviews %>%
  filter(str_detect(Text, "(?i)awesome|love|amazing"))

head(positive_reviews$Text, 5)
```

    ## [1] "Great taffy at a great price.  There was a wide assortment of yummy taffy.  Delivery was very quick.  If your a taffy lover, this is a deal."                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               
    ## [2] "This saltwater taffy had great flavors and was very soft and chewy.  Each candy was individually wrapped well.  None of the candies were stuck together, which did happen in the expensive version, Fralinger's.  Would highly recommend this candy!  I served it at a beach-themed party and everyone loved it!"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           
    ## [3] "This taffy is so good.  It is very soft and chewy.  The flavors are amazing.  I would definitely recommend you buying it.  Very satisfying!!"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               
    ## [4] "Right now I'm mostly just sprouting this so my cats can eat the grass. They love it. I rotate it around with Wheatgrass and Rye too"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        
    ## [5] "I don't know if it's the cactus or the tequila or just the unique combination of ingredients, but the flavour of this hot sauce makes it one of a kind!  We picked up a bottle once on a trip we were on and brought it back home with us and were totally blown away!  When we realized that we simply couldn't find it anywhere in our city we were bummed.<br /><br />Now, because of the magic of the internet, we have a case of the sauce and are ecstatic because of it.<br /><br />If you love hot sauce..I mean really love hot sauce, but don't want a sauce that tastelessly burns your throat, grab a bottle of Tequila Picante Gourmet de Inclan.  Just realize that once you taste it, you will never want to use any other sauce.<br /><br />Thank you for the personal, incredible service!"

<br>

For our last example, let’s find reviews that include some numbers in
them, specifically lets look at reviews that are related to product size
or include cooking measurements.

<br>

``` r
number_reviews <- reviews %>%
  filter(str_detect(Text,"\\d+\\s*(oz|lbs|ml|g|kg)"))

head(number_reviews$Text, 5)
```

    ## [1] "Grape gummy bears are hard to find in my area. In fact pretty much anyone I talk to about grape gummy bears they think I'm lying. So I bought 10lbs... : ) These bears are a little bit bigger then the other brands and have kind of sour kick, but nothing to strong. I love grape flavored candy/soda and these are pretty good. There is another company that makes grape gummy bears that are a little bit better in my opinion, but these are well worth it for the price. I like to use the gummy bears in home made Popsicles with flavored sports drink. The salt in the sports drink makes for softer popsicles, and the gummy bears are awesome frozen. They are delicious!"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
    ## [2] "I have been drinking Royal King 100% Natural Organic Green Tea (100 tea bags x 2g each) as my every day tea for several years now.  I buy 12 boxes at a time to save on shipping.  For many years I used to drink coffee from morning till night.  But finally I realized that drinking so much coffee was not healthy for me.  I finally resolved to improve my health and stopped drinking coffee all together.  I tried many alternative drinks to replace my coffee habit.  I found that green tea was not only good tasting it also has health benefits.  Green tea is one of the few drinks that actually makes you healthier (coffe and other drinks do not) - the only healthier drink is quality cold water.  In my opinion, for the price, Royal King 100% Natural Organic Green Tea is one of the best tasting teas.  This green tea has a beautiful golden color, the taste is bright and fresh.  I recommend adding a tiny amount of Y.S. Organic Bee Farms RAW HONEY to the tea to add sweetness and health benefits too.  I also give myself a treat once in a while by having a much more expense tea (Tribute Xi Hu Long Jing) but this fantastic tea is not practical for me to drink as my every day tea (although I would if I could afford it).<br /><br />Cons:  On my latest shipment the package shown on the Amazon page is different than the one shipped.  The one shipped displays \"NATURALLY HIGH IN POLYPHENOL CATECHINS\" (a key contributive element to the possible health effects of tea), whereas the Amazon package displays \"CAFFENE FREE\".  So I am not sure if this green tea is Caffene free or not.  The other con is that sometimes the tea bag rips open when I unwrap the string from around the tea bag. So if the string seems stuck to the tea bag I put the bag in the hot water to unstick it."
    ## [3] "The BEST investment I've ever made for ginger. It's unbelievable! It's fibrous like the real ginger, has that spicy kick to it, but it's perfect with the sugar - calms it down.  It's very worth the $40 for 5lbs of it!  I'll be getting more soon - I use these as a topper for my ginger cupcakes and cookies :)"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              
    ## [4] "I went to 4 grocery stores looking for this flavor of Jello for my green tomato jam recipe and finally found it here. This jello is wonderful! Evidently it's only carried in the stores during the summer but with harvest time in the Fall, I couldn't find it anywhere in town. This Jello tastes like watermelon and the jam recipe I made with it takes like watermelon jam! Great made as regular Jello too. Yummy!"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         
    ## [5] "We made chocolate chip cookies with BRM Garbanzo Bean Flour and the results were fantastic!  The brown sugar and chocolate mask any bean taste that other reviews have mentioned.  Our friends couldn't discern any difference from classic CCCs.  The texture, body, and elasticity (meaning reduced tendency to fall apart that occurs with most other gluten-free flours) is nice and chewy -- the same as CCCs made with regular flour.  And an added bonus -- the high protein and fiber level (I calculate 2-3 g fiber/cookie) fills you up so that you are satisfied with smaller servings and the glycemic index is significantly lower.<br /><br />I highly recommend this flour even if CCCs are the only thing you make with it."

<br>

Logic: - \d+ -\> Searches the reviews for one or more digits - \s\* -\>
matches zero or more spaces - (oz\|lbs\|ml\|g\|kg) -\> matches the units

The \s\* will be helpful incase reviews have “20oz” or “20 oz”.

<br>

*Step 3: Cleaning the Data*

As we’ve learned throughout this course, cleaning text data is necessary
before we conduct in-depth analysis.

Let’s start with removing any special characters or punctuations.

``` r
reviews <- reviews %>% mutate(Text = str_replace_all(Text, "[[:punct:]]", ""))
```

“\[\[:punct:\]\]” will remove any character like periods (.), commas
(,), exclamation points (!), etc.

Another thing that may be helpful in analysis is removing common words
or otherwise known as stopwords. These will remove words such as “the”
or “and”. These filler words don’t add much meaning to the content of
the revew.

<br>

``` r
# Note: This will take a very long time to process! 

# library(stopwords)

# Remove stopwords from text
# reviews <- reviews %>% 
  #mutate(Text = str_remove_all(Text, paste(stopwords("en"), collapse = "\\b|\\b")))

# Add word boundaries to prevent partial matches
# reviews <- reviews %>% 
  #mutate(Text = str_remove_all(Text, "\\b(\\s+|)\\b"))
```

Here is a helpful article on the stopwards package in R - [Stopwords
Package](https://cran.r-project.org/web/packages/stopwords/readme/README.html)

## Conclusion

Overall, getting comfortable with Regex will be helpful in your data
analytics journey as it allows you to clean, extract, and analyze text
data. This can be applied to a varied of field wheter you are reviewing
customer reviews, movie titles, or survey responses.

<br> <br>
