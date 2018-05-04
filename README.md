# deeptraffic
preserving some small js to graft new cloned layers between existing ones

net (8).js was not inspiring, but it seemed to do the right thing.  

i wanted to see what it would take to graft another layer without destroying the precious cobwebs it depends on.

net (10).js the reserialized edition of net8.js after the client loads it, showing that at least the js is doing what was intended if not the mechanics.

![image](https://user-images.githubusercontent.com/73514/39615013-09630958-4f9e-11e8-8bb8-9a1e92ae69ef.png)

code here
https://github.com/jnorthrup/deeptraffic/blob/e04a4ce356c24c5378189e7161a7faedaee9d51e/net%20(8).js#L141


![image](https://user-images.githubusercontent.com/73514/39614859-2f2f0ce6-4f9d-11e8-9e33-eb70b51c8f60.png)


re-uptake curve
===
curious but not surprising, this works, but not out of the box.  there seems to exist a short fitting cost for creating a new layer and bridging the old one.

the re-uptake curve looks a little bit like this, and takes about 1-2 minutes on my laptop training.

![image](https://user-images.githubusercontent.com/73514/39627564-84ca0650-4fd0-11e8-9ea9-76797d6c9083.png)

