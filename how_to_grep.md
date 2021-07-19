# How to grep

Find several patterns in a collection of files:
```bash
grep -E 'pattern1|pattern2' *.log 
```

Get all files with a certain name and grep in them:
```bash
find . -name "*.log" | xargs grep -E 'pattern1|pattern2'
```

Show x amount of line before or after the match:
```bash
grep 'pattern' -A {x} *.log
grep 'pattern' -B {x} *.log
```
