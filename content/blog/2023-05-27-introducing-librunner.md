+++
title = "Introducing LibRunner"
authors = ["Hildeberto Mendonca",]
description = "A good deal of being a geek is to code or understand coding. We love objectivity and hate subjectivity, so coding is the ultimate objectivity sophistication. If something can be expressed in numbers and logic, then code is the best way to materialize and document it. That's why we created a programming library where we can express all the calculations related to running and let other geeks use and contribute to."
+++

LibRunner is an open source library published on GitHub and distributed by create.io. We decided to write it in Rust for the following reasons:

* **Performance**: Rust is fast, compared to C, and often replacing C in production code due to its memory safety guarantees. The domain of sports often requires real-time features, so Rust allows calculations to be as fast as they can possibly be, without the uncertainties of garbage collection.

* **Popular**: Rust has been elected by a annual StackOverflow survey as the most loved language for 5 consecutive years. It has a large and strong community of users and contributors as well as a great number of sponsors, from small start-ups to global players, investing on the language and its ecosystem. It implements the state of the art on development experience, making developers happy about the process of building high performance software.

* **Reusable**: Publishing LibRunner on creates.io is so straightforward that we did it as soon as its first feature was available. Today, any Rust project can add it as a dependency and use it for running-related applications. In addition to that, LibRunner can also be used by other programming languages through bridges. We intend to support other languages on demand, ensuring the same underline logic across platforms and technologies. LibRunner can also be used on the browser thanks to the rich Rust support for WebAssembly.

* **High Level**, yet native, writing Rust code feels like writing in a high level language such as Kotlin, Scala, and C#. Yet, the result is native, platform specific, and self-contained software.

LibRunner currently offers the following features:

* given duration and distance, it calculates the average speed and pace to complete the distance within that duration.

* given duration and pace, calculates the distance of a race.

* given a set of splits, calculates the duration and distance of the race.

* calculates the pace of positive and negative splits of a race.

We are constantly improving and adding new features to it as we learn more about the field. We are also open to suggestions, demands, and contributions.

In the LibRunner documentation, we have examples of code for every feature. These examples are guaranteed to work because the Cargo testing tool runs them against the current version. You can copy and paste them into your code and make the necessary changes to the problem you are solving.

Let's go through quick steps to get start with LibRunner. We start a Rust project from zero to unlock they way to hero:

1. visit https://rustup.rs and install rustup, an installer for the programming language Rust. Once installed, update and check the toolchain:

       $ rustup update
       $ rustc --version
       $ cargo --version

2. create your new running application:

       $ cargo new runningapp

3. a folder called `runningapp` is created. Go into it and run the project:

       $ cd runningapp
       $ cargo run

4. it prints "Hello World", meaning you have a working code to start from. Open the project in your favourite code editor and make two changes: 

   4.1. add LibRunner to the project's dependencies in the file `Cargo.toml`:

      ```toml
      [dependencies]
      librunner = "0.4.0"
      ```

   4.2. replace the content of the file `src/main.rs` by the code below:

      ```rust
      use std::time::Duration;
      use librunner::running::{Race, MetricRace, ImperialRace};
      use librunner::utils::convert;

      fn main() {
          let duration = convert::to_duration(4, 0, 0); // 04:00:00
          let m_race: MetricRace = Race::new(42195, duration);
          let m_average_pace = m_race.average_pace();

          println!("The pace to run {}km in {}h is approximately {}.{}/km at {:.2}km/h", 
                   (m_race.distance as f32 / 1000.0), 
                   (duration.as_secs() / 60 / 60), 
                   (m_average_pace.as_secs() / 60),
                   (m_average_pace.as_secs() % 60),
                   (m_race.speed() * 3.6));

          let i_race: ImperialRace = Race::new(46112, duration);
          let i_average_pace = i_race.average_pace();

          println!("The pace to run {} miles in {}h is approximately {}.{}/mile at {:.2}mph", 
                   (i_race.distance as f32 / 1760.0), 
                   (duration.as_secs() / 60 / 60),
                   (i_average_pace.as_secs() / 60),
                   (i_average_pace.as_secs() % 60),
                   (i_race.speed() * 3.6));
      }
      ```
5. then run the project again:

       $ cargo run

    which generates the following output:

       The pace to run 42.195km in 4h is approximately 5.41/km at 10.55km/h
       The pace to run 26.2 miles in 4h is approximately 9.9/mile at 11.53mph

That's it! You are now using LibRunner in no time. Keep an eye on this website to learn more about future updates and all things geeks love about running.