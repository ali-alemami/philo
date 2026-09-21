*This project has been created as part of the 42 curriculum by aalemami.*

# philo

---

## Description

Philosophers is a concurrency project implementing the classic **Dining Philosophers Problem**. N philosophers sit at a round table, each with one fork, needing **two forks** to eat. Philosophers cycle between three states: **eating**, **sleeping**, and **thinking**. The simulation ends either when a philosopher dies of starvation, or when all philosophers have eaten a required number of times.

The goal is to manage philosopher threads without data races, deadlocks, or starvation, using **mutexes** to protect shared resources (forks).

---

## Instructions

### Compilation

Build the executable using `make`:

```bash
make
```

Additional Makefile rules:
```bash
make clean   # Remove object files
make fclean  # Remove object files and executable
make re      # Rebuild from scratch
```

### Usage

```bash
./philo <number_of_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [number_of_times_each_philosopher_must_eat]
```

| Argument | Description |
| :--- | :--- |
| `number_of_philosophers` | Number of philosophers (and forks) at the table |
| `time_to_die` (ms) | Time since a philosopher last started eating (or simulation start) before they die |
| `time_to_eat` (ms) | Time it takes to eat (holds two forks during this) |
| `time_to_sleep` (ms) | Time spent sleeping after eating |
| `number_of_times_each_philosopher_must_eat` | Optional — simulation stops when all philosophers reach this count |

### Output Format

Each event is printed with a millisecond timestamp:
```
<timestamp_in_ms> <philosopher_id> <action>
```
Where `action` is one of: `has taken a fork`, `is eating`, `is sleeping`, `is thinking`, or `died`.

### Examples

```bash
./philo 5 800 200 200          # 5 philosophers, should not die
./philo 1 800 200 200          # 1 philosopher, dies (only one fork available)
./philo 4 410 200 200          # tight timing, should not die
./philo 5 800 200 200 7        # stops after each philosopher eats 7 times
./philo 5 100 200 200          # time_to_die too short, philosopher dies
```

---

## Resources

- [POSIX Threads Programming — Lawrence Livermore National Laboratory](https://hpc-tutorials.llnl.gov/posix/)
- [The Dining Philosophers Problem — Wikipedia](https://en.wikipedia.org/wiki/Dining_philosophers_problem)
- [pthread_mutex_lock(3) — Linux man page](https://man7.org/linux/man-pages/man3/pthread_mutex_lock.3p.html)
- [gettimeofday(2) — Linux man page](https://man7.org/linux/man-pages/man2/gettimeofday.2.html)
- [Multithreading in C — GeeksForGeeks](https://www.geeksforgeeks.org/c/multithreading-in-c/)

### AI Usage

AI was used as a learning and development assistant for:
- Explaining `pthread` APIs (`pthread_create`, `pthread_join`, `pthread_detach`) and their lifecycle behaviors.
- Clarifying mutex initialization, locking, and destruction patterns (`pthread_mutex_init`, `pthread_mutex_destroy`).
- Precise timestamp calculations and sleep routines using `gettimeofday` to minimize timing drift.
- Reasoning about data race scenarios and shared state synchronization.
