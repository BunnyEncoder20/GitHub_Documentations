
# Chapter 1
- I already know about the forgetting curve 
![[Screenshot 2024-09-13 at 9.58.47 AM.png]]
- The most efficient way of making the learning curve more shallower is by **spaced repetition**. Basically spacing out the times when we see a question/card again.
- Anki calls the time between seeing the cards as *intervals*
- The interval size keeps increasing by a multiple of **2.5**. Basically the time between seeing the same question again increases by a factor of **2.5**.
- So the days pattern will look something like this 
![[Pasted image 20240913100814.png]]
- Anki not only uses these days intervals but also smaller intervals when the card is in the **learning phase** and has still not matured yet.
- Anki uses 4 buttons when we see a card : 
```
Again - forgot the card cmopletely 
Hard - Very difficult to remember 
Good - Easy to remember 
Easy - I already know this
```

---

# Chapter 2

- **Learning Phase** is when we see a new card for the first time.
- When we press the feedback buttons the following intervals occur after which the same card will be shown again: 
```
Again = 1 min
Hard = 5 min
Good = 10 min
```
- Once we click on good again after a 10 min interval, the card is set to be graduated (matured). And this day would be marked as the first day (day 1) of the card day intervals.
- A card is said to be forgotten when a graduated card is clicked using the "Again". This **resets** the cards and it needs to graduate again by getting "Good" after a 10 min interval.
- **However, once the card graduates this time, the interval factor is reduced by 0.2 (so 2.3).**
- The interval factor will keep on reducing each time a card is forgotten until it reaches the lower limit of *1.3*

---

# Chapter 3 - Questions to figure out

- What if someone doesn't see the cards on the designated day ?
- How to store the data related to the spaced repetition of each card/question efficiently in mongoDB