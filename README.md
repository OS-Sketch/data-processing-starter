# Data Processing

[![build](../../actions/workflows/build.yml/badge.svg)](../../actions/)
[![Language: Python](https://img.shields.io/badge/Language-Python-blue.svg)](https://www.python.org/)
[![Commits: Conventional](https://img.shields.io/badge/Commits-Conventional-blue.svg)](https://www.conventionalcommits.org/en/v1.0.0/)
[![Discord](https://img.shields.io/discord/1013818801281839184?logo=discord)](https://discord.gg/9VfCdqffu6)

## Introduction

This project introduces the steps that you must take to implement, build, and
run a Python program called `processor` that uses the `schedule` package to
implement a `cron`-like scheduling application that can start a `generator` and
a `summarizer` task that can, respectively, generate and summarize synthetic
data about audio files. The `generator` task will use the `Faker` package to
automatically generate realistic file names of audio files and then append these
names and randomly generated file sizes to a CSV file. The `summarizer` task
will read in all of the existing data about the audio files, compute the
arithmetic mean of the file sizes, and then write that out to the summary file.
For this project, `processor` will use the `data/generated.csv` file to contain
the data about the audio files and the `data/summary.csv` file to contain the
summarized information about the audio files.

As you complete this project, please review all of the contents of the following
references:

- Documentation for the `schedule` package: https://schedule.readthedocs.io/en/stable/
- Documentation for the `faker` package: https://faker.readthedocs.io/en/master/
- Article that explains the steps for creating virtual environments: https://realpython.com/python-virtual-environments-a-primer/
- Article that explains how to manipulate CSV files: https://realpython.com/python-csv/
- StackOverflow discussion about virtual environments: https://stackoverflow.com/questions/1871549/determine-if-python-is-running-inside-virtualenv

## Seeking Assistance

Even though the course instructor will have covered all of the concepts central
to this project before you start to work on it, please note that not every
detail needed to successfully complete the assignment will have been covered
during prior classroom sessions. This is by design as an important skill that
you must practice as you explore the depth and breadth in the field of operating
systems. If you have questions about this project, please schedule a meeting
with the course instructor during office hours.

## Program Implementation

Before you get started on this project, please use the `python` command to
create a virtual environment called `venv`. You will then need to use the `pip`
command to install the `schedule` and `faker` packagers. To learn more about the
commands that you should take to complete these steps, make sure to review all
of the references mention in the introduction for this project. After you have
installed all of the correct dependencies and implemented all of the required
source code, your `processor` program should support a command line like the
following: `venv/bin/python project/pylang/processor.py 10 3 5`. This is the way
in which you should interpret this listing of command-line arguments:

- `10`: the number of data generation rounds for which `processor` should run
- `3`: the data generation periodicity, in seconds, that controls the repeated
  execution of the `generator` task
- `5`: the data summarization periodicity, in seconds, that controls the
  repeated execution of the `summarizer` task

Bearing in mind that the program involves the use of random numbers, when you
run the program it would produce output like the following:

```text
process: Schedule data generation and processing

Summary of command-line arguments:
  Number of arguments: 4
  Name of the program: project/pylang/processor.py
  Data Generation maximum: 10 generation rounds
  Data generation periodicity: 3 seconds
  Data summarization periodicity: 5 seconds

Deleting any existing data or summary CSV files!
Starting to run the cron job scheduler!

Wed Oct 26 14:35:59 2022 Generating data
Wed Oct 26 14:36:01 2022 Summarizing data
Wed Oct 26 14:36:02 2022 Generating data
Wed Oct 26 14:36:05 2022 Generating data
Wed Oct 26 14:36:06 2022 Summarizing data
Wed Oct 26 14:36:08 2022 Generating data
Wed Oct 26 14:36:11 2022 Summarizing data
Wed Oct 26 14:36:11 2022 Generating data
Wed Oct 26 14:36:14 2022 Generating data
Wed Oct 26 14:36:16 2022 Summarizing data
Wed Oct 26 14:36:17 2022 Generating data
Wed Oct 26 14:36:20 2022 Generating data
Wed Oct 26 14:36:21 2022 Summarizing data
Wed Oct 26 14:36:23 2022 Generating data
Wed Oct 26 14:36:26 2022 Summarizing data
```

As you implement the `processor` program, please make sure that it addresses the
following issues:

- Make sure that `processor` deletes any existing files in the `data` directory
  before it starts to run the `cron`-like jobs that involve the `generator` and
  `summarizer` tasks.

- If the person running the `processor` presses `CTRL-c` during its execution,
  the program should cleanly exit instead of printing a stack trace. Ultimately,
  the `processor` program should always return an exit code of `0` unless the
  program encounters an unforeseen problem like a corrupted file.

- Each time `processor` runs a round of data generation, it should create `10`
  new files such that each one has a valid file name for an audio file and a
  file size of a numerical value representing the size in megabytes. For
  instance, the file `economic.wav` with a file size of `267` MB could be stored
  in the `data/generated.csv` file with the row `economic.wav,267`. All of the
  generated file sizes should be between `0` and `1024` MB. You should use the
  `faker` package to generate random, yet meaningful, audio file names.

- Each time `processor` runs a round of data generation, it should append the
  `10` rows of data, one for each file, to the `data/generate.csv` file. For a
  given run of `processor` across multiple rounds of data generation, the data
  should be appended to the file, thereby ensuring that no data is overwritten
  during the program's execution.

- Each time `processor` runs a round of data summarization, the `summarizer`
  task should read in all of the rows of data from the `data/generated.csv` file
  and compute the arithmetic mean of all of the file sizes in the input file.
  After computing the average file size, the `summarizer` task should append
  a row of data to the `data/summary.csv` that features one column with the
  total number of rows used to produce the average file size and another column
  with the computed average file size.

- Every time that `processor` runs either the `generator` or `summarizer` task
  it should output a diagnostic message that includes a human-readable
  timestamp for the time at which the task is run and then a label for whether
  the program was performing data generation or summarization.

- Before the `processor` programs uses the `schedule` package to start the
  `cron`-like `generator` and `summarizer` tasks it should parse all of the
  command-line arguments and then display them in a summary message. This means
  that every run of `processor` should produce output that makes it clear which
  command-line arguments it was provided before running the two tasks in the
  specified configuration.

Here is the contents of the `data/generated.csv` file after running the
`processor` in the aforementioned configuration:

```text
culture.mp3,955
position.wav,962
economic.wav,267
never.mp3,463
agree.wav,45
help.wav,298
hard.wav,381
picture.flac,295
clear.flac,924
everything.mp3,1022
truth.mp3,385
feel.wav,217
recently.wav,950
campaign.mp3,674
foreign.wav,383
office.flac,78
drug.mp3,58
alone.mp3,725
military.mp3,141
however.flac,499
simple.mp3,615
general.flac,810
summer.flac,834
tonight.wav,166
establish.wav,706
she.flac,274
find.mp3,463
shoulder.flac,461
know.flac,774
blood.flac,913
adult.wav,545
because.wav,384
good.flac,896
different.wav,376
together.wav,524
specific.wav,95
position.wav,104
unit.wav,155
budget.flac,532
religious.wav,871
mother.mp3,137
health.mp3,678
teacher.mp3,621
source.wav,343
thousand.wav,42
happen.wav,644
ok.wav,773
activity.mp3,480
general.mp3,540
fear.wav,92
scientist.wav,219
help.mp3,273
picture.flac,761
recognize.flac,917
away.wav,239
always.wav,1001
hour.flac,30
yes.flac,4
mission.flac,942
charge.flac,340
cell.flac,245
Mrs.flac,436
north.mp3,935
office.flac,530
whose.wav,756
partner.wav,98
put.mp3,652
in.wav,862
itself.flac,401
southern.mp3,228
stand.wav,156
item.wav,797
how.wav,264
wrong.flac,196
evening.mp3,97
off.flac,634
child.wav,404
memory.mp3,662
field.wav,742
worker.wav,979
improve.flac,854
hotel.wav,15
piece.wav,574
around.flac,513
quickly.mp3,622
seat.wav,786
until.mp3,1015
go.mp3,965
or.mp3,318
down.mp3,547
run.mp3,24
reality.wav,453
special.flac,879
society.flac,1015
leader.wav,64
do.wav,197
another.wav,713
learn.mp3,388
PM.flac,325
out.wav,752
```

Here is the contents of the `data/summary.csv` file after running the
`processor` in the aforementioned configuration:

```text
10,561.2
30,524.6
40,505.5
60,488.26666666666665
80,492.125
90,506.43333333333334
```

Before you dive into the implementation of the `processor` program, please make
sure that you understand why the specified command-line arguments caused the
program to produce the provided command-line output and files. If you have
questions about this project, please share them in a public channel of the
Discord server for this course.

### Project Reflection

As you work on this project, you should regularly take time to reflect on the
steps that you are taking and why you are taking them. Each time you run a
program you should think about the inputs, outputs, and behavior of that
program, jotting down notes to help you remember these insights. When you are
writing Python and Go programs, please reserve time to reflect on the features
of the language that you are learning and how the languages are similar to and
different from each other. As you complete this project, make sure that
you reflect on your own strengths and weaknesses and how you can improve in
advance of the next project. You should also reflect on the process that you
followed to find, consult, and leverage external resources that helped you to
implement the `processor` program.

### Automated Assessment

Please review the following notes about the way in which your project will be
automatically assess in GitHub Actions:

- If you have already installed the
  [GatorGrade](https://github.com/GatorEducator/gatorgrade) program that runs
  the automated grading checks provided by
  [GatorGrader](https://github.com/GatorEducator/gatorgrader) you can, from the
  repository's base directory, run the automated grading checks by typing
  `gatorgrade --config config/gatorgrade.yml`.
- You may also review the output from running GatorGrader in GitHub Actions.
- Don't forget to provide all of the required responses to the technical writing
  prompts in the `writing/reflection.md` file.
- Please make sure that you completely delete the `TODO` markers and their
  labels from all of the provided source code. This means that instead of only
  deleting the `TODO` marker from the code you should delete the `TODO` marker
  and the entire prompt and then add your own comments to demonstrate that you
  understand all of the source code in this project.
- Please make sure that you also completely delete the `TODO` markers and their
  labels from every line of the `writing/reflection.md` file. This means that
  you should not simply delete the `TODO` marker but instead delete the entire
  prompt so that your reflection is a document that contains polished technical
  writing that is suitable for publication on your professional web site.
- Please note that the `build.yml` file for this project is configured to run
  `gatorgrade` with the command `./venv/bin/gatorgrade --config
  config/gatorgrade.yml`. This means that your program must be setup so that it
  runs in a virtual environment called `venv` that contains all of the project's
  dependencies and that can support the installation and use of `gatorgrade`.
