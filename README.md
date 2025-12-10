# Mechanical Prime Sieve

An interactive 3D visualization of a mechanical prime number sieve, inspired by the Sieve of Eratosthenes.

I explain it in this three minute video: [https://youtu.be/5GF_pQyrpCs](https://youtu.be/5GF_pQyrpCs)

## How It Works

The visualization demonstrates a mechanical approach to finding prime numbers using rotating gears (discs):

1. **The Shaft (C₁)**: A rotating shaft drives all the gears. Each full rotation of the shaft increments the rotation counter R.

2. **Gears (Cₙ)**: Each gear Cₙ has:
   - A circumference proportional to n (so C₂ is twice as big as C₁, C₃ is three times as big, etc.)
   - An opaque slice covering 1/n of the disc
   - The rest of the disc is semi-transparent

3. **The Sieve Mechanism**:
   - Because gear Cₙ has n times the circumference of the shaft, it rotates 1/n as fast
   - The opaque slice blocks the "window" (green viewing tube) every n rotations
   - At rotation R, if R is divisible by n, the slice of Cₙ blocks the window

4. **Finding Primes**:
   - Look through the green viewing tube toward the yellow target
   - If you can see the yellow target (no opaque slice blocking), the window is **OPEN**
   - When the window is open at rotation k, and k is larger than all existing gears, k must be prime!
   - A new gear Cₖ is automatically added

## Controls

| Key | Action |
|-----|--------|
| **Space** | Pause / Resume |
| **R** | Restart (back to R=2 with only C₂) |
| **F** | Forward (normal direction) |
| **D** | Reverse (removes gears as you go back) |
| **V** | View through tube (camera looks through the green tube) |
| **Mouse** | Orbit camera / zoom |

## Running Locally

The visualization requires a local web server due to ES module imports. You can use any of these methods:

```bash
# Python 3
python3 -m http.server 8000

# Node.js (if you have npx)
npx serve .

# PHP
php -S localhost:8000
```

Then open `http://localhost:8000` in your browser.

## Visual Elements

- **Gray Shaft**: The main rotating axle (C₁)
- **Orange Crank**: Attached to the shaft to visualize rotation
- **Blue Discs**: The prime gears (C₂, C₃, C₅, C₇, ...)
- **Dark Blue Slices**: The opaque 1/n portion of each gear
- **Red Slices**: Indicates a gear is currently blocking the window
- **Green Tube**: The viewing window - look through here!
- **Yellow Target**: Visible when the window is open (prime found!)

## The Math

This is a physical representation of the Sieve of Eratosthenes:

- At R=2: Only C₂ exists, and it blocks (2 divides 2)
- At R=3: C₂ doesn't block (2 doesn't divide 3), window open → 3 is prime, add C₃
- At R=4: C₂ blocks (2 divides 4)
- At R=5: Neither C₂ nor C₃ blocks → 5 is prime, add C₅
- At R=6: Both C₂ and C₃ block (composite)
- At R=7: No gear blocks → 7 is prime, add C₇
- And so on...

## Technologies

- [Three.js](https://threejs.org/) for 3D rendering
- Vanilla JavaScript
- No build step required
