---
layout: post
title: "Building a MET Station Part 1"
date: 2024-01-26
---

Last summer, my wife & I decided that we want a garden, and to go with that garden, a greenhouse. Afterwards, I decided, to go with the greenhouse, a meteorological station. For a part of my job, I design and program embedded systems, usually open source ones. I thought that this would be a good opportunity to design a system to withstand harsh, outdoor conditions right outside my home. It is currently in the -40s and -50s (doesn't matter Celsius or Fahrenheit) here in the interior of Alaska. It doesn't get much colder than that. The summer highs almost never reach 100F, which most electronics don't mind. Rather, it's the cold that most electronics won't like. Of course, there's also moisture concerns, and even the possibility of lightning. Regarding the question of wildlife, I'm not concerned about moose since the station will be located inside an electric fence.

Those are my design constraints. *My modus operandi for this project is to have other engineers do as much of the work for me as possible.* That is, I'm not going to build my own temperature sensor; someone else has probably designed one that fits within my constraints. I do not want to deal with things like the [Steinhart-Hart equations](https://en.wikipedia.org/wiki/Steinhart%E2%80%93Hart_equation). I do enough of that for work and my enjoyment of this project is important to me.

That being said, with some feedback with some folks over at [the Alaskan Mastodon instance](https://alaskan.social/about) and the venerable Arctic climate specialist [Rick Thoman](https://substack.com/@alaskaclimate), whose climate and weather knowledge far surpass my own, here's what I have decided (or not) to measure, specked, and why:

- 2 meter subsurface temperature: [DS18B20](https://www.sparkfun.com/products/11050) for $11. It's waterproof. The probe will need conduit since it's not rated for pressure, but I'd rather have it that way in case there's a sensor malfunction and I need to retrieve it. The conduit will be thermally nonconductive as to avoid introducing some sort of bias.
- ~~surface soil moisture and~~ temperature: [DS18B20](https://www.sparkfun.com/products/11050). I can't find a soil moisture that is rated for the cold and is reasonable. As much as Rick recommended it (he said it once), I'm not going to do moisture.
- 3 meter temperate and relative humidity: [DS18B20](https://www.sparkfun.com/products/11050) & [SHT31-D](https://www.adafruit.com/product/2857) ($14). It's hard to go wrong with that DS18B20. The SHT31-D also does temperature, but it's rated to -40 and I do really want my temperatures working.
- barometric pressure: [LPS33HW](https://www.adafruit.com/product/4414) for $13. I'll need to design a case around this, but it's already water resistant. It's also rated to -40. Where I'm at, though, I haven't seen -40 since I'm a bit above the lowest points in the Fairbanks basin. It's a bit of a risk, but it's not as important (to me) as the temperature.
- pyranometer: [SP-230-SS](https://www.apogeeinstruments.com/sp-230-ss-all-season-heated-pyranometer/) for $230. It's all season and self heated. I might need to design a low gain amplifier though, but op-amps make things so easy.
- color sensor: [APDS9960](https://www.adafruit.com/product/3595) for $8. It has other things on it, but I just care about the RGB sensor. My thought process with this one is to get an average color of the day. Imagine what 365 colors of the day would look like. Or even the average color of the year.
- ~~liquid precipitation~~: Turns out they're a bit expensive. At least for this first iteration, they're going to be omitted. Sorry, Rick.
- ~~anemometer~~: There's trees where I'm at and the garden is right by a bluff. I also don't want to go above the trees. And zoning. And lightning.
- ~~GPS~~: As cool as it would be, it just means for math for me. I guess movement from permafrost that or that [earthquake](https://earthquake.alaska.edu/magnitude-53-earthquake-near-salcha-rattles-interior-alaska) would be cool, but I'm just not that interested in it.

Originally, I thought that I was going to use a [Adafruit Feather](https://www.adafruit.com/product/3178), but after looking at all the pins I'll be using, I might use a Metro although I'll lose that nice radio. They're is always muxes, I guess, but that's more designing. I think what I'll do is order the parts then count the wires and decide then.

Whatever I decide on, I know I'll need a few voltage regulators since some things are operating and separate voltages. Also, to try to avoid lightning or just electrical faults in general, optoisolators will be a good idea.

Until next time.