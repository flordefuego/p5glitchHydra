# p5glitchHydra
example of how to run p5glitch in Hydra.

![](https://raw.githubusercontent.com/ffd8/p5.glitch/master/includes/images/p5.glitch_ani.gif)

## [p5glitch](http://p5.glitch.me/) is a [p5.js](https://p5js.org/) library for glitching images and binary files in the web browser created by [Ted Davis](https://teddavis.org/)
This library must be loaded apart from p5js with Hydra's loadScript() function, then introduced with p5js.

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
glitch.loadQuality(0.1); //define glitch quality, the less quality, more glitches
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


