# After-effect-cheat-sheet

This markdown document provides a comprehensive cheat sheet for various After Effects animation transitions and effects. 


### 1. **Basic Fade In/Out**
**Opacity Keyframe Transition**
```jsx
// Fade In
thisComp.layer("LayerName").opacity.setValueAtTime(startTime, 0);
thisComp.layer("LayerName").opacity.setValueAtTime(endTime, 100);

// Fade Out
thisComp.layer("LayerName").opacity.setValueAtTime(startTime, 100);
thisComp.layer("LayerName").opacity.setValueAtTime(endTime, 0);
```

### 2. **Slide In/Out**
**Position Keyframe Transition**
```jsx
// Slide In from Left
thisComp.layer("LayerName").transform.position.setValueAtTime(startTime, [initialX, initialY]);
thisComp.layer("LayerName").transform.position.setValueAtTime(endTime, [finalX, finalY]);

// Slide Out to Right
thisComp.layer("LayerName").transform.position.setValueAtTime(startTime, [initialX, initialY]);
thisComp.layer("LayerName").transform.position.setValueAtTime(endTime, [finalX, finalY]);
```

### 3. **Scale Up/Down**
**Scale Keyframe Transition**
```jsx
// Scale Up
thisComp.layer("LayerName").transform.scale.setValueAtTime(startTime, [initialScale, initialScale]);
thisComp.layer("LayerName").transform.scale.setValueAtTime(endTime, [finalScale, finalScale]);

// Scale Down
thisComp.layer("LayerName").transform.scale.setValueAtTime(startTime, [initialScale, initialScale]);
thisComp.layer("LayerName").transform.scale.setValueAtTime(endTime, [finalScale, finalScale]);
```

### 4. **Rotation**
**Rotation Keyframe Transition**
```jsx
// Rotate
thisComp.layer("LayerName").transform.rotation.setValueAtTime(startTime, initialRotation);
thisComp.layer("LayerName").transform.rotation.setValueAtTime(endTime, finalRotation);
```

### 5. **Bounce Effect**
**Bounce Expression for Position**
```jsx
// Apply to Position
amp = 20; // Amplitude
freq = 2; // Frequency
decay = 5; // Decay
n = 0;
if (numKeys > 0){
    n = nearestKey(time).index;
    if (key(n).time > time){
        n--;
    }
}
if (n == 0){
    t = 0;
}else{
    t = time - key(n).time;
}
if (n > 0){
    v = velocityAtTime(key(n).time - thisComp.frameDuration/10);
    value + v*amp*Math.sin(freq*t*2*Math.PI)/Math.exp(decay*t);
}else{
    value;
}
```

### 6. **Wiggle Effect**
**Wiggle Expression for Random Motion**
```jsx
// Apply to any property, e.g., Position, Rotation
frequency = 5; // Frequency
magnitude = 20; // Magnitude
wiggle(frequency, magnitude);
```

### 7. **Opacity Blink**
**Opacity Expression for Blinking Effect**
```jsx
// Apply to Opacity
frequency = 2; // Frequency
if (Math.sin(time * frequency * Math.PI * 2) > 0) 100 else 0;
```

### 8. **Color Change Over Time**
**Color Expression for Changing Color**
```jsx
// Apply to Color
timeFactor = 1; // Speed of color change
sin(time * timeFactor * 2 * Math.PI) * 0.5 + 0.5;
```

### 9. **Loop Out**
**Looping Keyframes**
```jsx
// Loop Out for Position, Scale, Rotation, etc.
loopOut(type = "cycle", numKeyframes = 0);
```

### 10. **Custom Expression for Oscillating Motion**
**Custom Oscillation Expression**
```jsx
// Oscillation for any property, e.g., Position
freq = 2; // Frequency
amp = 50; // Amplitude
decay = 3; // Decay
angle = freq * time * 2 * Math.PI;
value + [Math.sin(angle) * amp / Math.exp(decay * time), 0];
```

### 11. **Elastic Scale Up**
**Elastic Scale Expression**
```jsx
// Apply to Scale
freq = 3; // Frequency of oscillation
decay = 5; // Decay rate
amp = 100; // Amplitude of the initial overshoot
t = time - inPoint;
startScale = 0; // Starting scale value

value + [amp * Math.exp(-decay * t) * Math.cos(freq * t * 2 * Math.PI), amp * Math.exp(-decay * t) * Math.cos(freq * t * 2 * Math.PI)];
```

### 12. **3D Flip**
**3D Rotation Transition**
```jsx
// Apply to Y Rotation (3D layer)
startRotation = 0;
endRotation = 180;
easeTime = linear(time, startTime, endTime, startRotation, endRotation);
```

### 13. **Circular Reveal**
**Circular Mask Expansion**
```jsx
// Use with a circular mask path keyframes
startRadius = 0;
endRadius = 1000;
mask("Mask 1").maskPath.setValueAtTime(startTime, ellipsePath(startRadius));
mask("Mask 1").maskPath.setValueAtTime(endTime, ellipsePath(endRadius));

function ellipsePath(radius) {
    var points = [];
    var pointsNum = 32;
    for (var i = 0; i < pointsNum; i++) {
        var angle = (i / pointsNum) * Math.PI * 2;
        points.push([Math.cos(angle) * radius, Math.sin(angle) * radius]);
    }
    return points;
}
```

### 14. **Typewriter Effect**
**Text Reveal Character by Character**
```jsx
// Apply to Source Text
delay = 0.1;
charIndex = Math.floor(time / delay);
substr(0, charIndex);
```

### 15. **Ripple Effect**
**Ripple Expression for Distortion**
```jsx
// Apply to Position or Scale for ripple-like effect
freq = 2; // Frequency of ripple
amp = 20; // Amplitude of ripple
decay = 2; // Decay rate

t = time - inPoint;
value + [Math.sin(freq * t * Math.PI * 2) * amp * Math.exp(-decay * t), 0];
```

### 16. **Shake Effect**
**Camera Shake Expression**
```jsx
// Apply to Position for shake effect
freq = 10; // Frequency of shake
amp = 20; // Amplitude of shake

wiggle(freq, amp);
```

### 17. **Directional Blur**
**Directional Blur Transition**
```jsx
// Apply to Directional Blur Effect
startBlurLength = 0;
endBlurLength = 50;
linear(time, startTime, endTime, startBlurLength, endBlurLength);
```

### 18. **3D Parallax Effect**
**Parallax Effect for Depth**
```jsx
// Apply to Position for a 3D parallax effect
camSpeed = 500; // Speed of the camera movement

xParallax = thisComp.layer("Camera 1").transform.position[0] * camSpeed / thisComp.width;
yParallax = thisComp.layer("Camera 1").transform.position[1] * camSpeed / thisComp.height;
value + [xParallax, yParallax];
```

### 19. **Layer Wiggle on Offbeat**
**Wiggle Expression Synced to Music Beats**
```jsx
// Apply to any property for wiggle synced to music
freq = 5; // Frequency of wiggle
amp = 50; // Amplitude of wiggle
beats = thisComp.layer("Audio Layer").effect("Sound Keys")("Output 1"); // Assuming using Sound Keys

wiggle(freq, amp * beats);
```

### 20. **Pulsating Effect**
**Scale Pulsation**
```jsx
// Apply to Scale for a pulsating effect
freq = 2; // Frequency of pulsation
amp = 10; // Amplitude of pulsation
startScale = 100; // Starting scale value

value + amp * Math.sin(freq * time * Math.PI * 2);
```

### 21. **Drop Shadow Wiggle**
**Drop Shadow for Dynamic Shadow Movement**
```jsx
// Apply to Drop Shadow properties for dynamic shadow movement
shadowDistance = 10;
shadowAngle = time * 360 / 5; // 5 seconds for a full rotation

shadowDistance = 10 + wiggle(2, 5);
shadowAngle = time * 360 / 5;
```

## 22. Zoom Blur
### Zoom Blur Effect
```jsx
// Apply to Zoom Blur Effect
startBlur = 0;
endBlur = 50;
linear(time, startTime, endTime, startBlur, endBlur);
```

## 23. Light Sweep
### Light Sweep Transition
```jsx
// Apply to Light Sweep Effect
startPosition = [0, value[1]];
endPosition = [thisComp.width, value[1]];
linear(time, startTime, endTime, startPosition, endPosition);
```

## 24. Page Turn
### Page Turn Effect
```jsx
// Apply to Page Turn Effect
startAngle = 0;
endAngle = 180;
linear(time, startTime, endTime, startAngle, endAngle);
```

## 25. Lens Distortion
### Lens Distortion Transition
```jsx
// Apply to Lens Distortion Effect
startDistortion = 0;
endDistortion = -100;
linear(time, startTime, endTime, startDistortion, endDistortion);
```

## 26. Glow Effect
### Glow Intensity Transition
```jsx
// Apply to Glow Effect
startGlow = 0;
endGlow = 100;
linear(time, startTime, endTime, startGlow, endGlow);
```

## 27. Radial Wipe
### Radial Wipe Transition
```jsx
// Apply to Radial Wipe Effect
startTransition = 0;
endTransition = 100;
linear(time, startTime, endTime, startTransition, endTransition);
```

## 28. Swipe Reveal
### Swipe Reveal with Position
```jsx
// Apply to Position
startPosition = [thisComp.width, value[1]];
endPosition = [value[0], value[1]];
linear(time, startTime, endTime, startPosition, endPosition);
```

## 29. Gaussian Blur
### Gaussian Blur Transition
```jsx
// Apply to Gaussian Blur Effect
startBlur = 0;
endBlur = 50;
linear(time, startTime, endTime, startBlur, endBlur);
```

## 30. Light Flicker
### Light Flicker Effect
```jsx
// Apply to Opacity
frequency = 10; // Flicker frequency
magnitude = 50; // Flicker magnitude
wiggle(frequency, magnitude);
```

## 31. Text Flicker
### Text Flicker Effect
```jsx
// Apply to Opacity of Text Layer
frequency = 15; // Flicker frequency
magnitude = 100; // Flicker magnitude
wiggle(frequency, magnitude);
```

## 32. Twirl Effect
### Twirl Effect Transition
```jsx
// Apply to Twirl Effect
startAngle = 0;
endAngle = 360;
linear(time, startTime, endTime, startAngle, endAngle);
```

## 33. Color Correction
### Color Correction Transition
```jsx
// Apply to Color Correction Effect (e.g., Exposure)
startExposure = 0;
endExposure = 2;
linear(time, startTime, endTime, startExposure, endExposure);
```

## 34. Motion Tile
### Motion Tile Transition
```jsx
// Apply to Motion Tile Effect
startOffset = [0, 0];
endOffset = [100, 0];
linear(time, startTime, endTime, startOffset, endOffset);
```

## 35. Polar Coordinates
### Polar Coordinates Transition
```jsx
// Apply to Polar Coordinates Effect
startInterpolation = 0;
endInterpolation = 100;
linear(time, startTime, endTime, startInterpolation, endInterpolation);
```

## 36. Saturation Change
### Saturation Transition
```jsx
// Apply to Hue/Saturation Effect
startSaturation = 0;
endSaturation = 100;
linear(time, startTime, endTime, startSaturation, endSaturation);
```

## 37. Tint Effect
### Tint Transition
```jsx
// Apply to Tint Effect
startTintAmount = 0;
endTintAmount = 100;
linear(time, startTime, endTime, startTintAmount, endTintAmount);
```

## 38. Wave Warp
### Wave Warp Transition
```jsx
// Apply to Wave Warp Effect
startWaveHeight = 0;
endWaveHeight = 50;
linear(time, startTime, endTime, startWaveHeight, endWaveHeight);
```

## 39. Echo Effect
### Echo Transition
```jsx
// Apply to Echo Effect
startNumberOfEchoes = 0;
endNumberOfEchoes = 10;
linear(time, startTime, endTime, startNumberOfEchoes, endNumberOfEchoes);
```

## 40. Corner Pin
### Corner Pin Transition
```jsx
// Apply to Corner Pin Effect
topLeft = linear(time, startTime, endTime, [0, 0], [100, 100]);
topRight = linear(time, startTime, endTime, [width, 0], [width - 100, 100]);
bottomLeft = linear(time, startTime, endTime, [0, height], [100, height - 100]);
bottomRight = linear(time, startTime, endTime, [width, height], [width - 100, height - 100]);
```



