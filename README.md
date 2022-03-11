# p5glitchHydra
example of how to run p5glitch in Hydra.

## [Hydra](https://hydra.ojack.xyz/) is a platform for live coding visuals, created by [Olivia Jack](https://ojack.xyz/).

## [p5glitch](http://p5.glitch.me/) is a [p5.js](https://p5js.org/) library for glitching images and binary files in the web browser created by [Ted Davis](https://teddavis.org/)
![](https://raw.githubusercontent.com/ffd8/p5.glitch/master/includes/images/p5.glitch_ani.gif)

This library must be loaded apart from p5js with Hydra's loadScript() function, then introduced with p5js.

![](https://github.com/flordefuego/p5glitchHydra/blob/main/hydra-2022-3-11-17.9.22.png?raw=true)

``` javascript
await loadScript("https://cdn.jsdelivr.net/npm/p5.glitch@latest/p5.glitch.js") //loads p5glitch library in Hydra

//generate a variable for glitch 
let glitch;

p = new P5() //load p5 in Hydra
glitch = new Glitch(p); //loads glitch lib. It's important to link p5's variable here (p).
//load any URL's image here
p.loadImage('https://upload.wikimedia.org/wikipedia/commons/1/1b/Triangulo_HSV.png', function(im) {
glitch.loadImage(im);
});

//this should be load before p5's draw function
glitch.loadType('jpg'); //define type of glitch file
glitch.loadQuality(0.1); //define glitch quality
p.imageMode(p.CENTER);

p.draw = () => {
	p.clear();
	glitch.resetBytes(); 
	glitch.replaceBytes(100, 104); 
	glitch.randomBytes(100);
	glitch.limitBytes(0.1);
	glitch.buildImage();
	p.image(glitch.image, p.width/2,p.height/2)
}
//hide p5's canvas
p.hide();

//load p5 source to use it in Hydra
s0.init({src: p.canvas}) 

osc(10).layer(src(s0).modulate(noise(2))).out()
```

## Try Hydra scketch [Here](https://hydra.ojack.xyz/?code=YXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGY2RuLmpzZGVsaXZyLm5ldCUyRm5wbSUyRnA1LmdsaXRjaCU0MGxhdGVzdCUyRnA1LmdsaXRjaC5qcyUyMiklMjAlMkYlMkZsb2FkcyUyMHA1Z2xpdGNoJTIwbGlicmFyeSUyMGluJTIwSHlkcmElMEElMEElMkYlMkZnZW5lcmF0ZSUyMGElMjB2YXJpYWJsZSUyMGZvciUyMGdsaXRjaCUyMCUwQWxldCUyMGdsaXRjaCUzQiUwQSUwQXAlMjAlM0QlMjBuZXclMjBQNSgpJTIwJTJGJTJGbG9hZCUyMHA1JTIwaW4lMjBIeWRyYSUwQWdsaXRjaCUyMCUzRCUyMG5ldyUyMEdsaXRjaChwKSUzQiUyMCUyRiUyRmxvYWRzJTIwZ2xpdGNoJTIwbGliLiUyMEl0J3MlMjBpbXBvcnRhbnQlMjB0byUyMGxpbmslMjBwNSdzJTIwdmFyaWFibGUlMjBoZXJlJTIwKHApLiUwQSUyRiUyRmxvYWQlMjBhbnklMjBVUkwncyUyMGltYWdlJTIwaGVyZSUwQXAubG9hZEltYWdlKCdodHRwcyUzQSUyRiUyRnVwbG9hZC53aWtpbWVkaWEub3JnJTJGd2lraXBlZGlhJTJGY29tbW9ucyUyRjElMkYxYiUyRlRyaWFuZ3Vsb19IU1YucG5nJyUyQyUyMGZ1bmN0aW9uKGltKSUyMCU3QiUwQWdsaXRjaC5sb2FkSW1hZ2UoaW0pJTNCJTBBJTdEKSUzQiUwQSUwQSUyRiUyRnRoaXMlMjBzaG91bGQlMjBiZSUyMGxvYWQlMjBiZWZvcmUlMjBwNSdzJTIwZHJhdyUyMGZ1bmN0aW9uJTBBZ2xpdGNoLmxvYWRUeXBlKCdqcGcnKSUzQiUyMCUyRiUyRmRlZmluZSUyMHR5cGUlMjBvZiUyMGdsaXRjaCUyMGZpbGUlMEFnbGl0Y2gubG9hZFF1YWxpdHkoMC4xKSUzQiUyMCUyRiUyRmRlZmluZSUyMGdsaXRjaCUyMHF1YWxpdHklMkMlMjB0aGUlMjBsZXNzJTIwcXVhbGl0eSUyQyUyMG1vcmUlMjBnbGl0Y2hlcyUwQXAuaW1hZ2VNb2RlKHAuQ0VOVEVSKSUzQiUwQSUwQXAuZHJhdyUyMCUzRCUyMCgpJTIwJTNEJTNFJTIwJTdCJTBBJTA5cC5jbGVhcigpJTNCJTBBJTA5Z2xpdGNoLnJlc2V0Qnl0ZXMoKSUzQiUyMCUwQSUwOWdsaXRjaC5yZXBsYWNlQnl0ZXMoMTAwJTJDJTIwMTA0KSUzQiUyMCUwQSUwOWdsaXRjaC5yYW5kb21CeXRlcygxMDApJTNCJTBBJTA5Z2xpdGNoLmxpbWl0Qnl0ZXMoMC4xKSUzQiUwQSUwOWdsaXRjaC5idWlsZEltYWdlKCklM0IlMEElMDlwLmltYWdlKGdsaXRjaC5pbWFnZSUyQyUyMHAud2lkdGglMkYyJTJDcC5oZWlnaHQlMkYyKSUwQSU3RCUwQSUyRiUyRmhpZGUlMjBwNSdzJTIwY2FudmFzJTBBcC5oaWRlKCklM0IlMEElMEElMkYlMkZsb2FkJTIwcDUlMjBzb3VyY2UlMjB0byUyMHVzZSUyMGl0JTIwaW4lMjBIeWRyYSUwQXMwLmluaXQoJTdCc3JjJTNBJTIwcC5jYW52YXMlN0QpJTIwJTBBJTBBb3NjKDEwKS5sYXllcihzcmMoczApLm1vZHVsYXRlKG5vaXNlKDIpKSkub3V0KCk=)

