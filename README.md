# Speech-to-Intent-MCU


Speech to Intent Model Training and Conversion to TensorFlow for Microcontrollers This model was developed to run on a Seeedstudio WIO Terminal with a ATSAMD51P19 MCU and ARM Cortex-M4F core The specifications can be found on Seeedstudio's website, current link is posted below: https://www.seeedstudio.com/wio-terminal

Before using this notebook, the following packages are necessary and can be installed with pip or conda It is recommended to run these in a virtual environment and/or with conda

    pip install pandas
    pip install numpy
    pip install librosa (for audio and music processing in Python)
    pip install audiomentations
    pip install tensorflow (various versions might be needed depending on your Python/Anaconda/Jupyter versions)

Goals of this project:

    As of January 2023, there is still not a considerable amount of support for FOSS speech recognition tasks that are capable of integrating with MCUs
    Microcontrollers are cheap and consume low amounts of energy
    WIO Terminal can be integrated with SBCs and other IoT devices for a plethora of use cases
    The other side of it is I just like playing with fancy software and electronics :)

Use Cases Beyond This One:

    Audio detection for home security (high decibel levels can be detected, noises can be classified into types (gunshots, glass breaking, dogs barking, etc.)
    Home automation - it is possible to control smart light bulbs, thermostats, washers and dryers, door locks, etc with additional hardware (WIO terminal comes with built in Wi-Fi connectivity and Raspberry Pi 40-pin compatibility.)

Constraints

    Large vocabularies cannot be implemented due to the RAM and flash constraints of MCUs

Background Context for Sound Processing

    Sound is nothing more than a vibration that propogates through a transmission medium (solid, liquid, gas)
    One molecule "pushes" another, that molucule pushes another and so on and so forth until it reaches another object
    Same principle applies to microphones -- A microphone has a diaphram that is pushed by sound waves and then returns to its origin position by a magnet -- This is then converted to an electrical signal (alternating current) which is proportional to sound amplitude (the louder the sound, the more the diaphram is pushed, and more current is produced) -- We record this with an analog to digital converter and record it in intervals -- Sampling rate = the number of times a reading is taken in one second - Hz are considered a cycle/second
    We can visualize audio signal as a graph of Amplitude (y-axis) vs Time (number of samples) -- This is not very helpful for analyzing sound -- Fourier transforms can be applied to decompose a singal into individual frequencies and the frequency's amplitude -- Multiple Fourier transforms can be applied and appended together to create a Spectrogram (Hz vs. Time) with color coded decibel levels
    Humans do not percieve frequencies in the linear scale
    We are better at detecting differences in lower frequencies (detecting 500 Hz vs 1000 Hz is easier than detecting 10,000 Hz and 10,500 Hz)
    Humans perception of sound range is about 20 Hz to 20,000 Hz
    The Mel scale was developed to place more weight on the frequencies that the human ear can hear

Overview of this Project

    Speech to intent directly converted to speech to parsed intent which is based on a predefined and specific domain vocabulary
    i.e. "Alexa, turn on the lights in the bedroom" this would get parsed into an output intent

