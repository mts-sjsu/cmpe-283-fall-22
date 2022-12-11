# CMPE 283 Fall 2022 Assignment 3

## Team
I did this assignment on my own.

---------- 

## Steps
1. Starting from assignment 2
2. I keep the original implementation for assignment 2, meaning I'm in effect double counting for the same result, but I think that's ok for the purpose of this assignment. I would like to have something working along the way of developing, so I did not modify any assignment 2 logic.
3. I decided to add a list like structure for storing different exit statistics. I built a linkedlist that will slowing grow when encountering new exit reason. The rest is just traverse through the list and triage the stats for different exit reason. Since the number of kinds of reason won't be too big, using this linked list shouldn't be too much worse than an array. Besides, I do not want to define empty spots for all possible exit reason, but later found out that some of those aren't used. I have also implemented a logic for both `0x4FFFFFFE` and `0x4FFFFFFF` to show all results when the value in `%ecx` does not match any existing stats
```c
// cpuid.h

struct exit_reason_count {
	u32 reason;
	u32 count;
	unsigned long long cycles;
	struct exit_reason_count* next;
};
```
4. Rerun the build steps of `modules` and `modules_install`, then run `qemu` to spin up an inner VM. Run cpuid in the inner VM to verify these information are implemented correctly. Note that the `-s` flag is used to assign value to `%ecx`
```sh
# Printing # of exit and cycles for 0
> cpuid -l 0x4FFFFFFE -s 0x00000000
> cpuid -l 0x4FFFFFFF -s 0x00000000

# Printing # of exit and cycles for all recorded exits
> cpuid -l 0x4FFFFFFE -s 0x4FFFFFFF
> cpuid -l 0x4FFFFFFF -s 0x4FFFFFFF
```

---------- 

## Results
| ID  | Reason | Exit Count  | 
|---|---|---|
| 0  | Exception or non-maskable interrupt  |11  | 
| 10  | CPUID attempted  | 57308  |
| 28  | Control-register accesses | 109241  |
| 29  | MOV DR  | 1  |
| 30  | I/O instruction | 1000885  |
| 31  | RDMSR  | 968  |
| 48  | EPT violation   | 10825  |
| 54  | WBINVD or WBNOINVD  | 6  |

| ID  | Reason | Cycles  | Cycles/exit |
|---|---|---|---|
| 0  | Exception or non-maskable interrupt  | 1400544 | 127322 |
| 10  | CPUID attempted | 35456104  | 619 |
| 28  | Control-register accesses | 105881081 | 969 |
| 29  | MOV DR | 7801 | 7801 |
| 30  | I/O instruction | 2410754341 | 2409 |
| 31  | RDMSR  | 3273238 | 3381 |
| 48  | EPT violation   | 294671600 | 27221 |
| 54  | WBINVD or WBNOINVD | 4225 | 704 |

---------- 

## Questions
1. Comment on the frequency of exits – does the number of exits increase at a stable rate? Or are there more exits performed during certain VM operations? Approximately how many exits does a full VM boot entail? 
   1. In my case a full VM boot takes about `800k - 900k` exits. This would take the user to login, and there're around `500k` more after logging in. 
   2. After logging in, the # of exit roughly increase at a stable rate when I did not perform any additional action. While testing, the only action I did in the inner VM was the `cpuid` command, thus there isn't much variation in the number of exits
2. Of the exit types defined in the SDM, which are the most frequent? Least?
   1. The most frequent one is the `I/O` instruction, and the least frequent is the `MOV DR`. 

## Screenshot of the Execution
Note that the upper window is the inner VM, and the lower window is the host VM with my custom CPUID implemented.
<img width="743" alt="Screen Shot 2022-12-11 at 02 26 37" src="https://user-images.githubusercontent.com/100324756/206931093-cf5af917-58a1-4153-84ee-f8d166386804.png">
