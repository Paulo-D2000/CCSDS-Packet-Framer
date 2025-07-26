# CCSDS-Packet-Framer

A CCSDS Concatenated Framer block for GNU Radio.

This block implements the standard CCSDS concatenated encoding chain:
- Fixed Length Framing (Up to 219 bytes)
- CRC32 Insertion
- Reed-Solomon encoding (RS(255,223))
- CCSDS scrambler
- CCSDS 32-bit syncword insertion
- Convolutional encoding (variable rate, constraint length 7)

## 🔧 Dependencies

This block **requires** [gr-satellites](https://github.com/daniestevez/gr-satellites), which provides a compatible CCSDS Concatenated Deframer for use in receive (RX) chains.

## 🧱 Processing Flow

```text
Bytes → Framing(Fixed size, 219-Padding Bytes) → CRC32(0x4C11DB7) → RS(223,255) → Scrambler(CCSDS) → Syncword(CCSDS: 0x1ACFFC1D) → Convolutional Encoder (R=1/2, K=7) → Puncturing (Rate) -> Bytes
```

## 📦 Available FEC Rates

The block supports standard convolutional code puncturing patterns:

| Rate | Puncturing Pattern    |
|------|------------------------|
| 1/2  | `11`                   |
| 2/3  | `1101`                 |
| 3/4  | `110110`               |
| 5/6  | `1101100110`           |
| 7/8  | `11010101100110`       |

## 🚀 Usage

Use this block in a GNU Radio flowgraph to generate CCSDS-compatible transmit frames.

- For **TX chains**, use this framer.
- For **RX chains**, use the [**CCSDS Concatenated Deframer**](https://gr-satellites.readthedocs.io/en/latest/components.html#ccsds-deframers) from `gr-satellites`. 

## 📊 Example Flowgraph

*Coming soon…*

## 📄 License

MIT License
