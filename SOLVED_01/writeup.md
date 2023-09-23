This challenge can be solved 2 ways, reading the code or via debugger.
you can either put a breakpoint on line 75 in the code: (or anyhwere after the rightGuess is initialized really)
```
 if (guessString === rightGuessString) {
                let flag = rightGuessString + '@flare-on.com';
                toastr.options.timeOut = 0;
                toastr.options.onclick = function() {alert(flag);}
        toastr.success('You guessed right! The flag is ' + flag);
```

when setting a breakpoint around here, you can step thru the code, and see that the correct word is assigned to the rightGuess variable.
You can also just manually see that the rightGuess is assigned from words.js, go into that file, and see the right line.
(i do not know if words.js available in the live version)
