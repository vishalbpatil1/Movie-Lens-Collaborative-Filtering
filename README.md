# Movie-Lens-Collaborative-Filtering
![img](https://github.com/vishalbpatil1/Movie-Lens-Collaborative-Filtering/blob/main/img_.png)

Wondered how Google comes up with movies that are similar to the ones you like? After reading this post you will be able to build one such recommendation system for yourself.

It turns out that there are (mostly) three ways to build a recommendation engine:

1. Popularity based recommendation engine
2. Content based recommendation engine
3. Collaborative filtering based recommendation engine

Now you might be thinking “That’s interesting. But, what are the differences between these recommendation engines?”. Let me help you out with that.

### Popularity based recommendation engine:

Perhaps, this is the simplest kind of recommendation engine that you will come across. The trending list you see in YouTube or Netflix is based on this algorithm. It keeps a track of view counts for each movie/video and then lists movies based on views in descending order(highest view count to lowest view count). Pretty simple but, effective. Right?


### Content based recommendation engine:

This type of recommendation systems, takes in a movie that a user currently likes as input. Then it analyzes the contents (storyline, genre, cast, director etc.) of the movie to find out other movies which have similar content. Then it ranks similar movies according to their similarity scores and recommends the most relevant movies to the user.

### Collaborative filtering based recommendation engine:

This algorithm at first tries to find similar users based on their activities and preferences (for example, both the users watch same type of movies or movies directed by the same director). Now, between these users(say, A and B) if user A has seen a movie that user B has not seen yet, then that movie gets recommended to user B and vice-versa. In other words, the recommendations get filtered based on the collaboration between similar user’s preferences (thus, the name “Collaborative Filtering”). One typical application of this algorithm can be seen in the Amazon e-commerce platform, where you get to see the “Customers who viewed this item also viewed” and “Customers who bought this item also bought” list.


Look at the following picture to get a better intuition over content based and collaborative filtering based recommendation systems-

<img src="http://www.codeheroku.com/static/blog/images/pid14_rs_diff.png">

Another type of recommendation system can be created by mixing properties of two or more types of recommendation systems. This type of recommendation systems are known as hybrid recommendation system.

In this article, we are going to implement a Content based recommendation system using the scikit-learn library.

### Finding the similarity

We know that our recommendation engine will be content based. So, we need to find similar movies to a given movie and then recommend those similar movies to the user. The logic is pretty straightforward. Right?

But, wait…. How can we find out which movies are similar to the given movie in the first place? How can we find out how much similar(or dissimilar) two movies are?

Let us start with something simple and easy to understand.

Suppose, you are given the following two texts:

Text A: London Paris London

Text B: Paris Paris London

How would you find the similarity between Text A and Text B?

Let’s analyze these texts….

1. Text A: Contains the word “London” 2 times and the word “Paris” 1 time.
2. Text B: Contains the word “London” 1 time and the word “Paris” 2 times.

Now, what will happen if we try to represent these two texts in a 2D plane (with “London” in X axis and “Paris” in Y axis)? Let’s try to do this.

It will look like this-

<img src="http://www.codeheroku.com/static/blog/images/pid14_text_2d_repr.png">

Here, the red vector represents “Text A” and the blue vector represents “Text B”.

Now we have graphically represented these two texts. So, now can we find out the similarity between these two texts?

The answer is “Yes, we can”. But, exactly how?

These two texts are represented as vectors. Right? So, we can say that two vectors are similar if the distance between them is small. By distance, we mean the angular distance between two vectors, which is represented by θ (theta). By thinking further from the machine learning perspective, we can understand that the value of cos θ makes more sense to us rather than the value of θ (theta) because, the cosine(or “cos”) function will map the value of θ in the first quadrant between 0 to 1 (Remember? cos 90° = 0 and cos 0° = 1 ).

And from high school maths, we can remember that there is actually a formula for finding out cos θ between two vectors. See the picture below-

<img src="http://www.codeheroku.com/static/blog/images/pid14_find_cos_theta.png">

Don’t get scared, we don’t need to implement the formula from scratch for finding out cos θ. We have our friend Scikit Learn to calculate that for us :)

Let’s see how we can do that.

At first, we need to have text A and B in our program:
