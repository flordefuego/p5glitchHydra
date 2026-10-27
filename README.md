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

### Try Hydra scketch [Here](https://hydra.ojack.xyz/?code=YXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGY2RuLmpzZGVsaXZyLm5ldCUyRm5wbSUyRnA1LmdsaXRjaCU0MGxhdGVzdCUyRnA1LmdsaXRjaC5qcyUyMiklMjAlMkYlMkZsb2FkcyUyMHA1Z2xpdGNoJTIwbGlicmFyeSUyMGluJTIwSHlkcmElMEElMEElMkYlMkZnZW5lcmF0ZSUyMGElMjB2YXJpYWJsZSUyMGZvciUyMGdsaXRjaCUyMCUwQWxldCUyMGdsaXRjaCUzQiUwQSUwQXAlMjAlM0QlMjBuZXclMjBQNSgpJTIwJTJGJTJGbG9hZCUyMHA1JTIwaW4lMjBIeWRyYSUwQWdsaXRjaCUyMCUzRCUyMG5ldyUyMEdsaXRjaChwKSUzQiUyMCUyRiUyRmxvYWRzJTIwZ2xpdGNoJTIwbGliLiUyMEl0J3MlMjBpbXBvcnRhbnQlMjB0byUyMGxpbmslMjBwNSdzJTIwdmFyaWFibGUlMjBoZXJlJTIwKHApLiUwQSUyRiUyRmxvYWQlMjBhbnklMjBVUkwncyUyMGltYWdlJTIwaGVyZSUwQXAubG9hZEltYWdlKCdodHRwcyUzQSUyRiUyRnVwbG9hZC53aWtpbWVkaWEub3JnJTJGd2lraXBlZGlhJTJGY29tbW9ucyUyRjElMkYxYiUyRlRyaWFuZ3Vsb19IU1YucG5nJyUyQyUyMGZ1bmN0aW9uKGltKSUyMCU3QiUwQWdsaXRjaC5sb2FkSW1hZ2UoaW0pJTNCJTBBJTdEKSUzQiUwQSUwQSUyRiUyRnRoaXMlMjBzaG91bGQlMjBiZSUyMGxvYWQlMjBiZWZvcmUlMjBwNSdzJTIwZHJhdyUyMGZ1bmN0aW9uJTBBZ2xpdGNoLmxvYWRUeXBlKCdqcGcnKSUzQiUyMCUyRiUyRmRlZmluZSUyMHR5cGUlMjBvZiUyMGdsaXRjaCUyMGZpbGUlMEFnbGl0Y2gubG9hZFF1YWxpdHkoMC4xKSUzQiUyMCUyRiUyRmRlZmluZSUyMGdsaXRjaCUyMHF1YWxpdHklMkMlMjB0aGUlMjBsZXNzJTIwcXVhbGl0eSUyQyUyMG1vcmUlMjBnbGl0Y2hlcyUwQXAuaW1hZ2VNb2RlKHAuQ0VOVEVSKSUzQiUwQSUwQXAuZHJhdyUyMCUzRCUyMCgpJTIwJTNEJTNFJTIwJTdCJTBBJTA5cC5jbGVhcigpJTNCJTBBJTA5Z2xpdGNoLnJlc2V0Qnl0ZXMoKSUzQiUyMCUwQSUwOWdsaXRjaC5yZXBsYWNlQnl0ZXMoMTAwJTJDJTIwMTA0KSUzQiUyMCUwQSUwOWdsaXRjaC5yYW5kb21CeXRlcygxMDApJTNCJTBBJTA5Z2xpdGNoLmxpbWl0Qnl0ZXMoMC4xKSUzQiUwQSUwOWdsaXRjaC5idWlsZEltYWdlKCklM0IlMEElMDlwLmltYWdlKGdsaXRjaC5pbWFnZSUyQyUyMHAud2lkdGglMkYyJTJDcC5oZWlnaHQlMkYyKSUwQSU3RCUwQSUyRiUyRmhpZGUlMjBwNSdzJTIwY2FudmFzJTBBcC5oaWRlKCklM0IlMEElMEElMkYlMkZsb2FkJTIwcDUlMjBzb3VyY2UlMjB0byUyMHVzZSUyMGl0JTIwaW4lMjBIeWRyYSUwQXMwLmluaXQoJTdCc3JjJTNBJTIwcC5jYW52YXMlN0QpJTIwJTBBJTBBb3NjKDEwKS5sYXllcihzcmMoczApLm1vZHVsYXRlKG5vaXNlKDIpKSkub3V0KCk=)

## Example using animated gif
#### gif solution provided by Ted Davis

``` javascript

await loadScript("https://cdn.jsdelivr.net/npm/p5.glitch@latest/p5.glitch.js")

p = new P5() //comment this line after evaluating once
glitch = new Glitch(p); 
img = p.loadImage('https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExdTkwenozaTltNmlpNDl3cWR6dTF5b2xpajhwM25wcXZvMzA4NjlmbSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/fxO5urhnGImBuYtph7/giphy.gif', function(im) {
glitch.loadImage(im);
});

glitch.loadType('webp'); 
glitch.loadQuality(0.1); //define glitch quality
p.imageMode(p.CENTER);
p.frameRate(30)
p.hide() 

p.pixelDensity(1)

s0.init({ src: p.canvas } )
p.draw = () => {
	//glitch.limitBytes(p.abs(p.sin(p.frameCount))*0.8+0.5);
    img.setFrame(p.floor(p.frameCount)%img.numFrames())
  	glitch.loadImage(img);
	glitch.randomBytes(20,100);
    glitch.limitBytes(p.sin(p.frameCount)*0.4+0.4);
	glitch.buildImage();
  glitch.image.mask(img)
  //p.orbitControl()
	glitch.resetBytes(); 
	glitch.replaceBytes(1, 104); 
  p.image(glitch.image, p.width/2,p.height/2)
  
  }
//hide p5's canvas
p.hide();

//load p5 source to use it in Hydra
s0.init({src: p.canvas}) 

solid(0,0,1).layer(src(s0).modulate(noise(2))).out()
```
### open in [hydra editor](https://hydra.ojack.xyz/?code=JTBBYXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGY2RuLmpzZGVsaXZyLm5ldCUyRm5wbSUyRnA1LmdsaXRjaCU0MGxhdGVzdCUyRnA1LmdsaXRjaC5qcyUyMiklMEElMEFwJTIwJTNEJTIwbmV3JTIwUDUoKSUyMCUyRiUyRmNvbW1lbnQlMjB0aGlzJTIwbGluZSUyMGFmdGVyJTIwZXZhbHVhdGluZyUyMG9uY2UlMEFsZXQlMjBoYyUyMCUzRCUyMGRvY3VtZW50LmdldEVsZW1lbnRCeUlkKCdoeWRyYS1jYW52YXMnKSUwQWdsaXRjaCUyMCUzRCUyMG5ldyUyMEdsaXRjaChwKSUzQiUyMCUwQWltZyUyMCUzRCUyMHAubG9hZEltYWdlKCdodHRwcyUzQSUyRiUyRm1lZGlhMC5naXBoeS5jb20lMkZtZWRpYSUyRnYxLlkybGtQVGM1TUdJM05qRXhkVGt3ZW5vemFUbHRObWxwTkRsM2NXUjZkVEY1YjJ4cGFqaHdNMjV3Y1hadk16QTROamxtYlNabGNEMTJNVjlwYm5SbGNtNWhiRjluYVdaZllubGZhV1FtWTNROVp3JTJGZnhPNXVyaG5HSW1CdVl0cGg3JTJGZ2lwaHkuZ2lmJyUyQyUyMGZ1bmN0aW9uKGltKSUyMCU3QiUwQWdsaXRjaC5sb2FkSW1hZ2UoaW0pJTNCJTBBJTdEKSUzQiUwQSUwQWdsaXRjaC5sb2FkVHlwZSgnd2VicCcpJTNCJTIwJTBBZ2xpdGNoLmxvYWRRdWFsaXR5KDAuMSklM0IlMjAlMkYlMkZkZWZpbmUlMjBnbGl0Y2glMjBxdWFsaXR5JTBBcC5pbWFnZU1vZGUocC5DRU5URVIpJTNCJTBBcC5mcmFtZVJhdGUoMzApJTBBcC5oaWRlKCklMjAlMEElMEFwLnBpeGVsRGVuc2l0eSgxKSUwQSUwQXMwLmluaXQoJTdCJTIwc3JjJTNBJTIwcC5jYW52YXMlMjAlN0QlMjApJTBBcC5kcmF3JTIwJTNEJTIwKCklMjAlM0QlM0UlMjAlN0IlMEElMDklMkYlMkZnbGl0Y2gubGltaXRCeXRlcyhwLmFicyhwLnNpbihwLmZyYW1lQ291bnQpKSowLjglMkIwLjUpJTNCJTBBJTIwJTIwJTIwJTIwaW1nLnNldEZyYW1lKHAuZmxvb3IocC5mcmFtZUNvdW50KSUyNWltZy5udW1GcmFtZXMoKSklMEElMjAlMjAlMDlnbGl0Y2gubG9hZEltYWdlKGltZyklM0IlMEElMDlnbGl0Y2gucmFuZG9tQnl0ZXMoMjAlMkMxMDApJTNCJTBBJTIwJTIwJTIwJTIwZ2xpdGNoLmxpbWl0Qnl0ZXMocC5zaW4ocC5mcmFtZUNvdW50KSowLjQlMkIwLjQpJTNCJTBBJTA5Z2xpdGNoLmJ1aWxkSW1hZ2UoKSUzQiUwQSUyMCUyMGdsaXRjaC5pbWFnZS5tYXNrKGltZyklMEElMjAlMjAlMkYlMkZwLm9yYml0Q29udHJvbCgpJTBBJTA5Z2xpdGNoLnJlc2V0Qnl0ZXMoKSUzQiUyMCUwQSUwOWdsaXRjaC5yZXBsYWNlQnl0ZXMoMSUyQyUyMDEwNCklM0IlMjAlMEElMjAlMjBwLmltYWdlKGdsaXRjaC5pbWFnZSUyQyUyMHAud2lkdGglMkYyJTJDcC5oZWlnaHQlMkYyKSUwQSUyMCUyMCUwQSUyMCUyMCU3RCUwQSUyRiUyRmhpZGUlMjBwNSdzJTIwY2FudmFzJTBBcC5oaWRlKCklM0IlMEElMEElMkYlMkZsb2FkJTIwcDUlMjBzb3VyY2UlMjB0byUyMHVzZSUyMGl0JTIwaW4lMjBIeWRyYSUwQXMwLmluaXQoJTdCc3JjJTNBJTIwcC5jYW52YXMlN0QpJTIwJTBBJTBBc29saWQoMCUyQzAlMkMxKS5sYXllcihzcmMoczApLm1vZHVsYXRlKG5vaXNlKDIpKSkub3V0KCk%3D)

### example using p5.js on WEBGL mode

``` javascript
await loadScript("https://cdn.jsdelivr.net/npm/p5.glitch@latest/p5.glitch.js")

p = new P5({mode:'WEBGL'}) //comment this line after evaluating once

glitch = new Glitch(p); 
img = p.loadImage('https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExdTkwenozaTltNmlpNDl3cWR6dTF5b2xpajhwM25wcXZvMzA4NjlmbSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/fxO5urhnGImBuYtph7/giphy.gif', function(im) {
//glitch.loadImage(im);
});

glitch.loadType('png'); 
glitch.loadQuality(0.9); //define glitch quality
p.imageMode(p.CENTER);
p.frameRate(30)
p.hide() 

p.pixelDensity(1)

s0.init({ src: p.canvas } )
p.draw = () => {
  p.background(0,0,0,0); //gives transparency to the p5.js canvas when using WEBGL mode
    img.setFrame(p.floor(p.frameCount)%img.numFrames())
  	glitch.loadImage(img);
	glitch.randomBytes(104,100);
    glitch.limitBytes(p.sin(p.frameCount)*0.4+0.4);
	glitch.buildImage();
  	glitch.image.mask(img)
  //	p.orbitControl()
	glitch.resetBytes(); 
	glitch.replaceBytes(1, 104); 
  	p.noStroke();
  	p.rotateX(p.frameCount*0.05)
  	p.rotateY(p.frameCount*0.05)
  	p.texture(glitch.image);
  	p.box(200,500,50)
  
  }
//hide p5's canvas
p.hide();

//load p5 source to use it in Hydra
s0.init({src: p.canvas}) 

solid(0,0,1).layer(src(s0)).modulate(src(o0),0.01).out()
```

### open in [hydra editor](https://hydra.ojack.xyz/?code=JTBBYXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGY2RuLmpzZGVsaXZyLm5ldCUyRm5wbSUyRnA1LmdsaXRjaCU0MGxhdGVzdCUyRnA1LmdsaXRjaC5qcyUyMiklMEElMEFwJTIwJTNEJTIwbmV3JTIwUDUoJTdCbW9kZSUzQSdXRUJHTCclN0QpJTIwJTJGJTJGY29tbWVudCUyMHRoaXMlMjBsaW5lJTIwYWZ0ZXIlMjBldmFsdWF0aW5nJTIwb25jZSUwQSUwQWdsaXRjaCUyMCUzRCUyMG5ldyUyMEdsaXRjaChwKSUzQiUyMCUwQWltZyUyMCUzRCUyMHAubG9hZEltYWdlKCdodHRwcyUzQSUyRiUyRm1lZGlhMC5naXBoeS5jb20lMkZtZWRpYSUyRnYxLlkybGtQVGM1TUdJM05qRXhkVGt3ZW5vemFUbHRObWxwTkRsM2NXUjZkVEY1YjJ4cGFqaHdNMjV3Y1hadk16QTROamxtYlNabGNEMTJNVjlwYm5SbGNtNWhiRjluYVdaZllubGZhV1FtWTNROVp3JTJGZnhPNXVyaG5HSW1CdVl0cGg3JTJGZ2lwaHkuZ2lmJyUyQyUyMGZ1bmN0aW9uKGltKSUyMCU3QiUwQSUyRiUyRmdsaXRjaC5sb2FkSW1hZ2UoaW0pJTNCJTBBJTdEKSUzQiUwQSUwQWdsaXRjaC5sb2FkVHlwZSgncG5nJyklM0IlMjAlMEFnbGl0Y2gubG9hZFF1YWxpdHkoMC45KSUzQiUyMCUyRiUyRmRlZmluZSUyMGdsaXRjaCUyMHF1YWxpdHklMEFwLmltYWdlTW9kZShwLkNFTlRFUiklM0IlMEFwLmZyYW1lUmF0ZSgzMCklMEFwLmhpZGUoKSUyMCUwQSUwQXAucGl4ZWxEZW5zaXR5KDEpJTBBJTBBczAuaW5pdCglN0IlMjBzcmMlM0ElMjBwLmNhbnZhcyUyMCU3RCUyMCklMEFwLmRyYXclMjAlM0QlMjAoKSUyMCUzRCUzRSUyMCU3QiUwQSUyMCUyMHAuYmFja2dyb3VuZCgwJTJDMCUyQzAlMkMwKSUzQiUyMCUyRiUyRmdpdmVzJTIwdHJhbnNwYXJlbmN5JTIwdG8lMjB0aGUlMjBwNS5qcyUyMGNhbnZhcyUyMHdoZW4lMjB1c2luZyUyMFdFQkdMJTIwbW9kZSUwQSUyMCUyMCUyMCUyMGltZy5zZXRGcmFtZShwLmZsb29yKHAuZnJhbWVDb3VudCklMjVpbWcubnVtRnJhbWVzKCkpJTBBJTIwJTIwJTA5Z2xpdGNoLmxvYWRJbWFnZShpbWcpJTNCJTBBJTA5Z2xpdGNoLnJhbmRvbUJ5dGVzKDEwNCUyQzEwMCklM0IlMEElMjAlMjAlMjAlMjBnbGl0Y2gubGltaXRCeXRlcyhwLnNpbihwLmZyYW1lQ291bnQpKjAuNCUyQjAuNCklM0IlMEElMDlnbGl0Y2guYnVpbGRJbWFnZSgpJTNCJTBBJTIwJTIwJTA5Z2xpdGNoLmltYWdlLm1hc2soaW1nKSUwQSUyMCUyMCUyRiUyRiUwOXAub3JiaXRDb250cm9sKCklMEElMDlnbGl0Y2gucmVzZXRCeXRlcygpJTNCJTIwJTBBJTA5Z2xpdGNoLnJlcGxhY2VCeXRlcygxJTJDJTIwMTA0KSUzQiUyMCUwQSUyMCUyMCUwOXAubm9TdHJva2UoKSUzQiUwQSUyMCUyMCUwOXAucm90YXRlWChwLmZyYW1lQ291bnQqMC4wNSklMEElMjAlMjAlMDlwLnJvdGF0ZVkocC5mcmFtZUNvdW50KjAuMDUpJTBBJTIwJTIwJTA5cC50ZXh0dXJlKGdsaXRjaC5pbWFnZSklM0IlMEElMjAlMjAlMDlwLmJveCgyMDAlMkM1MDAlMkM1MCklMEElMjAlMjAlMEElMjAlMjAlN0QlMEElMkYlMkZoaWRlJTIwcDUncyUyMGNhbnZhcyUwQXAuaGlkZSgpJTNCJTBBJTBBJTJGJTJGbG9hZCUyMHA1JTIwc291cmNlJTIwdG8lMjB1c2UlMjBpdCUyMGluJTIwSHlkcmElMEFzMC5pbml0KCU3QnNyYyUzQSUyMHAuY2FudmFzJTdEKSUyMCUwQSUwQXNvbGlkKDAlMkMwJTJDMSkubGF5ZXIoc3JjKHMwKSkubW9kdWxhdGUoc3JjKG8wKSUyQzAuMDEpLm91dCgp)

### example using p5.js on WEBGL mode with an OBJ file

``` javascript

await loadScript("https://cdn.jsdelivr.net/npm/p5.glitch@latest/p5.glitch.js")

p = new P5({mode:'WEBGL'}) //comment this line after evaluating once

glitch = new Glitch(p); 
img = p.loadImage('https://media0.giphy.com/media/v1.Y2lkPTc5MGI3NjExdTkwenozaTltNmlpNDl3cWR6dTF5b2xpajhwM25wcXZvMzA4NjlmbSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/fxO5urhnGImBuYtph7/giphy.gif', function(im) {
//glitch.loadImage(im);
});

glitch.loadType('jpg'); 
glitch.loadQuality(0.9); //define glitch quality
p.imageMode(p.CENTER);
p.frameRate(30)
p.hide() 

//load obj file
let mushroom = p.loadModel('https://raw.githubusercontent.com/flordefuego/test_to_upload_stuff/main/hongo.obj', true);
p.pixelDensity(1)

s0.init({ src: p.canvas } )
p.draw = () => {
  p.background(0,0,0,0); //gives transparency to the p5.js canvas when using WEBGL mode
    img.setFrame(p.floor(p.frameCount)%img.numFrames())
  	glitch.loadImage(img);
	glitch.randomBytes(104,100);
    glitch.limitBytes(p.sin(p.frameCount)*0.4+0.4);
	glitch.buildImage();
  	glitch.image.mask(img)
  //	p.orbitControl()
	glitch.resetBytes(); 
	glitch.replaceBytes(1, 104); 
  	p.noStroke();
  	p.rotateY(p.frameCount*0.05);
  	p.scale(4)
  	p.texture(glitch.image);
  	p.model(mushroom);
  
  }
//hide p5's canvas
p.hide();

//load p5 source to use it in Hydra
s0.init({src: p.canvas}) 

solid(0,0,0.4).layer(src(s0)).out()
```
### open in [hydra editor](https://hydra.ojack.xyz/?code=JTBBYXdhaXQlMjBsb2FkU2NyaXB0KCUyMmh0dHBzJTNBJTJGJTJGY2RuLmpzZGVsaXZyLm5ldCUyRm5wbSUyRnA1LmdsaXRjaCU0MGxhdGVzdCUyRnA1LmdsaXRjaC5qcyUyMiklMEElMEFwJTIwJTNEJTIwbmV3JTIwUDUoJTdCbW9kZSUzQSdXRUJHTCclN0QpJTIwJTJGJTJGY29tbWVudCUyMHRoaXMlMjBsaW5lJTIwYWZ0ZXIlMjBldmFsdWF0aW5nJTIwb25jZSUwQSUwQWdsaXRjaCUyMCUzRCUyMG5ldyUyMEdsaXRjaChwKSUzQiUyMCUwQWltZyUyMCUzRCUyMHAubG9hZEltYWdlKCdodHRwcyUzQSUyRiUyRm1lZGlhMC5naXBoeS5jb20lMkZtZWRpYSUyRnYxLlkybGtQVGM1TUdJM05qRXhkVGt3ZW5vemFUbHRObWxwTkRsM2NXUjZkVEY1YjJ4cGFqaHdNMjV3Y1hadk16QTROamxtYlNabGNEMTJNVjlwYm5SbGNtNWhiRjluYVdaZllubGZhV1FtWTNROVp3JTJGZnhPNXVyaG5HSW1CdVl0cGg3JTJGZ2lwaHkuZ2lmJyUyQyUyMGZ1bmN0aW9uKGltKSUyMCU3QiUwQSUyRiUyRmdsaXRjaC5sb2FkSW1hZ2UoaW0pJTNCJTBBJTdEKSUzQiUwQSUwQWdsaXRjaC5sb2FkVHlwZSgnanBnJyklM0IlMjAlMEFnbGl0Y2gubG9hZFF1YWxpdHkoMC45KSUzQiUyMCUyRiUyRmRlZmluZSUyMGdsaXRjaCUyMHF1YWxpdHklMEFwLmltYWdlTW9kZShwLkNFTlRFUiklM0IlMEFwLmZyYW1lUmF0ZSgzMCklMEFwLmhpZGUoKSUyMCUwQSUwQSUyRiUyRmxvYWQlMjBvYmolMjBmaWxlJTBBbGV0JTIwbXVzaHJvb20lMjAlM0QlMjBwLmxvYWRNb2RlbCgnaHR0cHMlM0ElMkYlMkZyYXcuZ2l0aHVidXNlcmNvbnRlbnQuY29tJTJGZmxvcmRlZnVlZ28lMkZ0ZXN0X3RvX3VwbG9hZF9zdHVmZiUyRm1haW4lMkZob25nby5vYmonJTJDJTIwdHJ1ZSklM0IlMEFwLnBpeGVsRGVuc2l0eSgxKSUwQSUwQXMwLmluaXQoJTdCJTIwc3JjJTNBJTIwcC5jYW52YXMlMjAlN0QlMjApJTBBcC5kcmF3JTIwJTNEJTIwKCklMjAlM0QlM0UlMjAlN0IlMEElMjAlMjBwLmJhY2tncm91bmQoMCUyQzAlMkMwJTJDMCklM0IlMjAlMkYlMkZnaXZlcyUyMHRyYW5zcGFyZW5jeSUyMHRvJTIwdGhlJTIwcDUuanMlMjBjYW52YXMlMjB3aGVuJTIwdXNpbmclMjBXRUJHTCUyMG1vZGUlMEElMjAlMjAlMjAlMjBpbWcuc2V0RnJhbWUocC5mbG9vcihwLmZyYW1lQ291bnQpJTI1aW1nLm51bUZyYW1lcygpKSUwQSUyMCUyMCUwOWdsaXRjaC5sb2FkSW1hZ2UoaW1nKSUzQiUwQSUwOWdsaXRjaC5yYW5kb21CeXRlcygxMDQlMkMxMDApJTNCJTBBJTIwJTIwJTIwJTIwZ2xpdGNoLmxpbWl0Qnl0ZXMocC5zaW4ocC5mcmFtZUNvdW50KSowLjQlMkIwLjQpJTNCJTBBJTA5Z2xpdGNoLmJ1aWxkSW1hZ2UoKSUzQiUwQSUyMCUyMCUwOWdsaXRjaC5pbWFnZS5tYXNrKGltZyklMEElMjAlMjAlMkYlMkYlMDlwLm9yYml0Q29udHJvbCgpJTBBJTA5Z2xpdGNoLnJlc2V0Qnl0ZXMoKSUzQiUyMCUwQSUwOWdsaXRjaC5yZXBsYWNlQnl0ZXMoMSUyQyUyMDEwNCklM0IlMjAlMEElMjAlMjAlMDlwLm5vU3Ryb2tlKCklM0IlMEElMjAlMjAlMDlwLnJvdGF0ZVkocC5mcmFtZUNvdW50KjAuMDUpJTNCJTBBJTIwJTIwJTA5cC5zY2FsZSg0KSUwQSUyMCUyMCUwOXAudGV4dHVyZShnbGl0Y2guaW1hZ2UpJTNCJTBBJTIwJTIwJTA5cC5tb2RlbChtdXNocm9vbSklM0IlMEElMjAlMjAlMEElMjAlMjAlN0QlMEElMkYlMkZoaWRlJTIwcDUncyUyMGNhbnZhcyUwQXAuaGlkZSgpJTNCJTBBJTBBJTJGJTJGbG9hZCUyMHA1JTIwc291cmNlJTIwdG8lMjB1c2UlMjBpdCUyMGluJTIwSHlkcmElMEFzMC5pbml0KCU3QnNyYyUzQSUyMHAuY2FudmFzJTdEKSUyMCUwQSUwQXNvbGlkKDAlMkMwJTJDMC40KS5sYXllcihzcmMoczApKS5vdXQoKQ%3D%3D)
