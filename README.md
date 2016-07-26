-balabala
嘿哈，呀~~~吃我一剑

AE表达式
Keyframe Overshoot
freq = 3;
decay = 5;
n = 0;
if (numKeys > 0){
  n = nearestKey(time).index;
  if (key(n).time > time) n--;
}
if (n > 0){
  t = time - key(n).time;
  amp = velocityAtTime(key(n).time - .001);
  w = freq*Math.PI*2;
  value + amp*(Math.sin(t*w)/Math.exp(decay*t)/w);
}else
  value


...........................


Keyframe Bounce Back
e = .7;
g = 5000;
nMax = 9;
n = 0;
if (numKeys > 0){
  n = nearestKey(time).index;
  if (key(n).time > time) n--;
}
if (n > 0){
  t = time - key(n).time;
  v = -velocityAtTime(key(n).time - .001)*e;
  vl = length(v);
  if (value instanceof Array){
    vu = (vl > 0) ? normalize(v) : [0,0,0];
  }else{
    vu = (v < 0) ? -1 : 1;
  }
  tCur = 0;
  segDur = 2*vl/g;
  tNext = segDur;
  nb = 1; // number of bounces
  while (tNext < t && nb <= nMax){
    vl *= e;
    segDur *= e;
    tCur = tNext;
    tNext += segDur;
    nb++
  }
  if(nb <= nMax){
    delta = t - tCur;
    value +  vu*delta*(vl - g*delta/2);
  }else{
    value
  }
}else  value

