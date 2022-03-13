# My First Meme
### *A Practical Tutorial*
***

The meme I decided to create does not necessarilly follow a specific "meme format". I wanted to develop the kind of gif that is used as a **response** to something (*eg. what would typically be found in the comment section of a post on social media*). <br>
Memes are a form of comunication; they say a lot about a person's interests, their socio-economic standing, or even mental well-being. They express something that is relatable or understood beyond what is literally depicted. My meme is inspired by **vintage arcade games** and the trending **indie game scene** that often uses pixel art. It is a style that feels familiar and gives the perceiver a sense of nostalgia or childishness.
![Old Favourite, Zelda](https://upload.wikimedia.org/wikipedia/en/3/3a/Legend_of_Zelda_NES.PNG) <br>
https://zelda.fandom.com/wiki/The_Legend_of_Zelda
![Indie Game INMOST (Highly Recommend)](https://www.destructoid.com/wp-content/uploads/2020/12/569328-Inmost1.jpg)
https://inmostgame.com/ 

A common reaction to posts on social media nowadays are to be shocked or embarassed. I came up with the idea of showing a health bar declining, followed by a *"game over"* in a typical 80s style, im hopes that it would make for a good reaction meme that is easily interpreted and feels familiar.

>## DED 💔 💀 💀
>![Game Over Meme](Game_Over.gif) <br>
>~Random Comment

### To build my GIF meme I took the following steps:
* define coloured blocks to use as pixels
* append these blocks of coloured pixels to a vector of 'pixels'
* stack the rows to create a vector of 'pixel rows' that completes the image
* append full images in a row to mimic a health bar
* create the right combinations of images to animate later
* crop and color edit a background image from the internet
* annotate text over stylised background
* animate the final combination of images

### Below is the code I used with the [{magick}](https://cran.r-project.org/web/packages/magick/vignettes/intro.html) to make my meme:
```
library(magick)

#'pixel' dimensions
s_height = 30` <br>
s_width = 30` <br>
```

**1. Setting colors:**
```
red_square = image_blank(s_width, s_height, color = "#ff0000")
dark_square = image_blank(s_width, s_height, color = "#870000")
bl_square = image_blank(s_width, s_height, color = "#000000")
w_square = image_blank(s_width, s_height, color = "#ffffff")
```

**2. Creating rows of "pixels" for first heart:**
```
w_row = c(w_square, w_square, w_square, w_square, w_square,
          w_square, w_square, w_square, w_square) %>%
  image_append()

row_1 = c(w_square, w_square, bl_square, bl_square, w_square,
          bl_square, bl_square, w_square, w_square) %>%
  image_append()

row_2 = c(w_square, bl_square, red_square, red_square, bl_square,
          red_square, w_square, bl_square, w_square) %>%
  image_append()

row_3 = c(w_square, bl_square, red_square, red_square, red_square,
          red_square, red_square, bl_square, w_square) %>%
  image_append()

row_4 = c(w_square, w_square, bl_square, red_square, red_square,
          red_square, bl_square, w_square, w_square) %>%
  image_append()

row_5 = c(w_square, w_square, w_square, bl_square, red_square,
          bl_square, w_square, w_square, w_square) %>%
  image_append()

row_6 = c(w_square, w_square, w_square, w_square, bl_square,
          w_square, w_square, w_square, w_square) %>%
  image_append()
```


**3. First completed heart:**
```
heart_1 = c(w_row, row_1, row_2, row_3, row_4, row_5, row_6, w_row) %>%
  image_append(stack = TRUE) %>%
  image_scale(100)
```


**4. A darker heart to make it seem like it's beating:**
```
#Rows for dark heart
w_row = c(w_square, w_square, w_square, w_square, w_square,
          w_square, w_square, w_square, w_square) %>%
  image_append()

row_1a = row_1

row_2a = c(w_square, bl_square, dark_square, dark_square, bl_square,
           dark_square, w_square, bl_square, w_square) %>%
  image_append()

row_3a = c(w_square, bl_square, dark_square, dark_square, dark_square,
           dark_square, dark_square, bl_square, w_square) %>%
  image_append()

row_4a = c(w_square, w_square, bl_square, dark_square, dark_square,
           dark_square, bl_square, w_square, w_square) %>%
  image_append()

row_5a = c(w_square, w_square, w_square, bl_square, dark_square,
           bl_square, w_square, w_square, w_square) %>%
  image_append()

row_6a = c(w_square, w_square, w_square, w_square, bl_square,
           w_square, w_square, w_square, w_square) %>%
  image_append()
```


**5. Completed dark heart:**
```
dark_heart = c(w_row, row_1a, row_2a, row_3a, row_4a, row_5a, row_6a, w_row) %>%
  image_append(stack = TRUE) %>%
  image_scale(100)
```


**6. To do the heart-popping effect, I will need to create three extra images to replace the heart with when it disappears:**
```
#Rows for heart 2
row_2b = c(w_square, w_square, bl_square, bl_square, w_square,
           bl_square, bl_square, w_square, w_square) %>%
  image_append()

row_3b = c(w_square, w_square, bl_square, red_square, red_square,
           red_square, bl_square, w_square, w_square) %>%
  image_append()

row_4b = c(w_square, w_square, w_square, bl_square,
           red_square, bl_square, w_square, w_square, w_square) %>%
  image_append()

row_5b = row_6a
```

```
#Smaller heart #1
heart_2 = c(w_row, w_row, row_2b, row_3b, row_4b, row_5b, w_row, w_row) %>%
  image_append(stack = TRUE) %>%
  image_scale(100)
```


**7. Here are the rows for heart 3 (aka. smaller heart #2):**
```
row_2c = row_2b

row_3c = c(w_square, w_square, bl_square, bl_square, bl_square,
           bl_square, bl_square, w_square, w_square) %>%
  image_append()

row_4c = c(w_square, w_square, w_square, bl_square, bl_square,
           bl_square, w_square, w_square, w_square) %>%
  image_append()

row_5c = row_6a
```


**8. Smaller heart #2:**
```
heart_3 = c(w_row, w_row, row_2c, row_3c, row_4c, row_5c, w_row, w_row) %>%
  image_append(stack = TRUE) %>%
  image_scale(100)
```


**9. Here are the rows for heart 4 (black heart):**
```
row_1d = c(w_square, w_square, bl_square, w_square, w_square,
           w_square, bl_square, w_square, w_square) %>%
  image_append()

row_2d = c(w_square, w_square, w_square, bl_square,
           w_square, bl_square, w_square, w_square, w_square) %>%
  image_append()

row_3d = c(w_square, w_square, w_square, w_square, bl_square,
           w_square, w_square, w_square, w_square) %>%
  image_append()

row_4d = row_2d

row_5d = row_1d
```


**10. Black heart and empty heart:**
```
heart_4 = c(w_row, row_1d, row_2d, row_3d, row_4d, row_5d, w_row, w_row) %>%
  image_append(stack = TRUE) %>%
  image_scale(100)

#Empty heart
heart_5 = c(w_row, w_row, w_row, w_row, w_row, w_row, w_row, w_row)
```


**11. Generating 13 health-bars to animate later:**
``` 
health_bar_1 = image_append(c(heart_1, heart_1, heart_1))

health_bar_2 = image_append(c(dark_heart, dark_heart, heart_2))
health_bar_3 = image_append(c(heart_1, heart_1, heart_3))

health_bar_4 = image_append(c(dark_heart, dark_heart, heart_4))
health_bar_5 = image_append(c(heart_1, heart_1, heart_5))

health_bar_6 = image_append(c(dark_heart, heart_2, heart_5))
health_bar_7 = image_append(c(heart_1, heart_3, heart_5))

health_bar_8 = image_append(c(dark_heart, heart_4, heart_5))
health_bar_9 = image_append(c(heart_1, heart_5, heart_5))

health_bar_10 = image_append(c(heart_2, heart_5, heart_5))
health_bar_11 = image_append(c(heart_3, heart_5, heart_5))
health_bar_12 = image_append(c(heart_4, heart_5, heart_5))
health_bar_13 = image_append(c(heart_5, heart_5, heart_5))
```


**12. GAME OVER annotation and empty image for lightning effect:**
```
message = "GAME OVER"

lightning = image_read(path = "Images/Lightning_Bolt.png")  %>%
  image_scale(300) %>%
  image_crop("300x100") %>%
  image_negate() %>%
  image_annotate(message, gravity = "center", size = "40", weight = 700,
                 font = "Georgia", color = "#ffee00") 


empty_1 = image_blank(color = "#1900ff", width = 300, height = 100)
```

**13. Compiling everything to finally animate and save .gif:**
```
#Final Animation:
frames <- c(health_bar_1, health_bar_2, health_bar_3, health_bar_4, health_bar_5,
            health_bar_6, health_bar_7, health_bar_8, health_bar_9, health_bar_10,
            health_bar_11, health_bar_12, health_bar_13,
            lightning, empty_1, lightning, empty_1, lightning, lightning, lightning)

game_over = image_animate(frames, fps = 5)
game_over
image_write(game_over, path = "Images/Game_Over.gif", format = "gif")``
```

### This is my final result
![Game Over Meme](Game_Over.gif)
