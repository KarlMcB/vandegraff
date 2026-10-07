# Van de Graaff Lab

A Van de Graaff generator simulator for high school physics. It runs the 21 demonstrations from the *Van de Graaff Demonstrations* teacher guide (Demo 0 through 8.3) and adds a free-play bench.

Everything is in one file, `index.html`. There is nothing to install or build.

## Using it

Open `index.html` in a browser (Chrome on a Chromebook is the target), or host the folder on any static web server.

Each guided demo has three stages:

1. **Predict.** The bench is locked until the student commits to an answer.
2. **Test.** The procedure from the teacher guide, as a checklist that ticks itself off as the student does each step on the bench.
3. **Explain.** How the prediction did, what was seen, and why, in the language of the class slides (with slide numbers).

Controls worth knowing about:

- **Dome charges − / +** at the top sets the machine's polarity. Set it to match the class machine. Demo 0 ignores it on purpose (the polarity is a mystery to solve), and Demo 6.1 sets it from the roller material.
- **Show charges** draws electrons and protons. Bold symbols are unbalanced charge; faint pairs are balanced. Protons never move.
- **Touch wand to dome** grounds the dome without dragging.
- **Sound** is off by default.
- Progress (which demos are done) is kept in the browser's local storage on that device.

You can link straight to a demo by adding its number to the address, for example `index.html#5.2`, or to free play with `index.html#free`.

## Demos

| # | Demo | Part |
|---|------|------|
| 0 | Polarity Check ★ | Do this first |
| 1.1 | Meet the Electron Pump ★ | Charged vs. uncharged objects |
| 2.1 | Flying Pie Tins ★ | Charge interactions |
| 2.2 | Tissue-Paper Hair ★ | Charge interactions |
| 2.3 | Mystery Balloons | Charge interactions |
| 3.1 | Metal vs. Plastic Discharge ★ | Conductors & insulators |
| 3.2 | The Human Conductor | Conductors & insulators |
| 4.1 | The Rolling Soda Can ★ | Polarization |
| 4.2 | Bending Water | Polarization |
| 5.1 | Two-Can Induction ★ | Charging by induction |
| 5.2 | Charging an Electroscope by Induction ★ | Charging by induction |
| 5.3 | Electrophorus Station | Charging by induction |
| 6.1 | Look Inside the Machine ★ | Charging by friction |
| 6.2 | Build Your Own Series | Charging by friction |
| 6.3 | Where Did the Other Charge Go? | Charging by friction |
| 7.1 | Attract, Touch, Repel ★ | Charging by conduction |
| 7.2 | Charge-Sharing Sphere ★ | Charging by conduction |
| 7.3 | Puffed-Rice Fountain | Charging by conduction |
| 8.1 | The Spark ★ | Grounding |
| 8.2 | Plastic Straw vs. Foil Straw ★ | Grounding |
| 8.3 | Glowing Fluorescent Tube | Grounding |

★ = core demo in the teacher guide.

## What the model does and does not do

The physics is qualitative. Directions, signs and the order of events are right; magnitudes are tuned so effects are easy to see on a small screen.

- Hanging objects feel a Coulomb force from net charge plus an always-attractive force for polarization, which is why a neutral object is pulled toward anything charged.
- Conductors share charge on contact, polarize near a charged object, and drain to ground through a conducting path. Insulators keep their charge where it is.
- Induction follows the bookkeeping: grounding a conductor near a charged object leaves it with the opposite charge once the ground is removed first.
- Sparks jump when the gap is shorter than about 8 cm × the dome's charge fraction.
- Not modeled: humidity, charge leaking from sharp points, and real voltages or currents. Nothing here is a substitute for the safety rules in the teacher guide.

## The triboelectric series

Demos 6.1 and 6.2 use this order (top loves electrons most and becomes negative):

Teflon, Vinyl (PVC), Polyethylene, Styrofoam, Rubber, Cotton, Paper, Silk, Wool, Nylon, Human hair, Acrylic, Glass, Rabbit fur

It agrees with every pair in the guided notes (Teflon/rabbit fur, vinyl/paper, rubber/hair, silk/glass, polyethylene/wool, Styrofoam/cotton, and cotton above wool). If the ladder on slide 42 orders anything differently, edit the `SERIES` array near the top of the script in `index.html`.

## For developers

The script in `index.html` is organized as: utilities, the `World` and `Vdg` classes, the props (things on the bench), the `DEMOS` array, then the page logic. Each demo is one object in `DEMOS` with its prediction questions, a `setup` function that places props, and `steps` whose `ok` functions decide when a step is complete.

`window.VDG` is a small test hook. In the console, `VDG.start('7.1'); VDG.begin(); VDG.run(5)` loads a demo, skips the prediction and advances the simulation five seconds.
