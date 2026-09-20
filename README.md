# GNU Radio – BPSK/QPSK Data & File Transfer Experiments

This repository contains a collection of **GNU Radio Companion (GRC)** experiments exploring digital communication using **BPSK and QPSK**, packetized data transmission, text/file transfer, channel simulation, and SDR-based communication. The experiments progress from basic digital modulation and signal visualization to complete transmitter/receiver chains using packet formatting, CRC checking, synchronization, and USRP-based RF transmission and reception.

---

## 🛠️ Setup

These experiments were developed using **GNU Radio Companion** and SDR hardware such as **Ettus USRP**.

For GNU Radio installation and SDR configuration, refer to:

**[📄 Radioconda Installation Guide](./radioconda-installation-guide.pdf)**


---

# 📡 Experiments

## 1. QPSK Digital Modulation — `QPSK.grc`

This experiment demonstrates a basic **QPSK digital modulation system** using a random byte source and a QPSK constellation. The generated symbols are passed through a Root Raised Cosine filtering stage, with GNU Radio QT GUI blocks used to observe the signal before and after filtering. Constellation diagrams, eye diagrams, time-domain plots, and frequency-domain plots are provided to visualize the effect of pulse shaping and understand the characteristics of a QPSK signal.

---

## 2. Packet-Based Data Processing — `Packet_Virtual.grc`

This experiment introduces **packetized data transmission in GNU Radio** using virtual connections rather than an RF channel. A file source provides the input data, which is divided into tagged packets and processed using CRC and protocol formatting blocks. An access-code correlation stage is used to identify packets at the receiving side, followed by bit repacking and CRC verification before writing the recovered data to a file. QT GUI time sinks are also included to observe the transmitted and recovered packet data.

---

## 3. Basic BPSK Transmitter — `BPSK123.grc`

This experiment demonstrates a basic **BPSK signal generation and transmission chain**. A byte vector is converted into complex BPSK symbols using a chunks-to-symbols block and then passed through an interpolation FIR filter for pulse shaping and sample-rate increase. The resulting signal is mixed with a complex sinusoidal carrier and transmitted using a **UHD USRP Sink**. Constellation, time-domain, and eye-diagram visualizations are included to observe the generated BPSK signal at different stages of the transmitter.

---

## 4. BPSK Text File Transmitter — `Text_Tranfer_TXBPSK.grc`

This experiment implements a **BPSK transmitter for text-file transfer**. A text file is read as byte data, divided into payload packets, and combined with preamble and postamble information. CRC processing and GNU Radio protocol formatting are used to construct the packet structure before the data is passed to a BPSK constellation modulator. The resulting complex signal is scaled, visualized, and transmitted using a **UHD USRP Sink**. This flowgraph demonstrates how ordinary text data can be converted into a packetized BPSK RF signal.

---

## 5. BPSK Text File Receiver — `Text_Tranfer_RXBPSK.grc`

This experiment implements the corresponding **BPSK text-file receiver**. A UHD USRP Source captures the received complex RF signal, which is processed using an FFT Root Raised Cosine filter, symbol synchronization, and a Costas loop for timing and carrier recovery. The recovered symbols are decoded using a BPSK constellation decoder and differential decoder, followed by access-code correlation and CRC verification. The recovered byte stream is then written to a text file, completing the BPSK text-transfer receiver chain.

---

## 6. BPSK File Transfer with USRP Loopback — `Bpsk_file_transfer_loopback.grc`

This experiment combines the BPSK transmitter and receiver into a **USRP-based file-transfer loopback system**. A file is converted into packetized data with a preamble, payload, postamble, CRC, and protocol header before BPSK modulation and transmission through a UHD USRP Sink. The transmitted signal is received through a UHD USRP Source and processed using RRC filtering, symbol synchronization, Costas-loop carrier recovery, constellation decoding, differential decoding, access-code correlation, and CRC checking. The recovered bytes are finally written to a receive file, allowing the complete digital communication chain to be tested through an RF/USRP loopback setup.

---

## 7. BPSK File Transfer with Channel Simulation — `Bpsk_file_transfer5.grc`

This experiment extends the BPSK file-transfer system by introducing a **simulated communication channel** between the transmitter and receiver. The file is packetized and BPSK modulated before passing through a GNU Radio channel model. The channel model provides adjustable **noise, frequency offset, and time offset**, allowing the effect of common communication impairments to be investigated. At the receiver, RRC filtering, symbol synchronization, Costas-loop carrier recovery, constellation decoding, differential decoding, access-code detection, and CRC verification are used to recover the original file. GUI controls allow the channel impairments to be changed during the experiment.

---

## 8. BPSK Video/File Transmitter — `File_Video_Transmitter.grc`

This experiment demonstrates the transmission of a **video file as packetized BPSK data** using a USRP. A video file is read as a byte stream and divided into payload packets with configurable preamble and postamble sections. CRC processing and protocol formatting are applied before the data is passed to a BPSK constellation modulator operating at a configurable samples-per-symbol rate. The resulting complex signal is scaled, displayed using time-domain and constellation GUI sinks, and transmitted through a **UHD USRP Sink**. The flowgraph is configured with a sample rate of **1 MS/s** and a default RF frequency of **905.2 MHz**.

---

## 9. BPSK Video Receiver — `BPSK_video_receiver_RTL.grc`

This experiment implements the **BPSK receiver corresponding to the video/file transmitter**. A UHD USRP Source captures the received signal at the configured RF frequency, after which RRC filtering, symbol synchronization, Costas-loop carrier recovery, BPSK constellation decoding, differential decoding, access-code correlation, and CRC verification are performed. The recovered byte stream is written to a file, while constellation, frequency-domain, and time-domain GUI sinks provide visualization of the received signal. The flowgraph is configured for a **1 MS/s sample rate**, a default frequency of **905.2 MHz**, and an adjustable receive gain.

> **Note:** Although the flowgraph filename contains `RTL`, the uploaded flowgraph uses a **UHD USRP Source**, not an RTL-SDR Source.

---

