# AwesomeChasm
Chasm: The Rift PC game resource collection.

## Links
- [Chasm: The Rift Archive](https://www.chasm3d.com/)
- [Chasm: The Rift Modding Wiki](https://moddingwiki.shikadi.net/wiki/Chasm:_The_Rift)
- [Chasm: The Rift - Website Recreation by Effektus](http://chasm.atspace.eu/)

## Ports
- [Chasm-Reverse Panzerchasm](https://github.com/Panzerschrek/Chasm-Reverse)
- [OpenChasm](https://github.com/alexey-lysiuk/OpenChasm)
- [Chasm: The Rift Portable Staging](https://www.moddb.com/games/chasm-the-rift/downloads/chasm-portable-staging)
- [Chasm: The Rift Demo](https://www.gog.com/en/game/chasmtherift_demo)

## Models
- [Chasm: The Rift - 3OVIEW.EXE DOS model viewer](https://www.chasm3d.com/files/dump/CDEMOf.zip)
- [Noesis .3O/.CAR 3D model viewer/converter](https://richwhitehouse.com/index.php?content=inc_stream.php)

## Music
- [Chasm: The Rift - FLAC OST music](https://www.chasm3d.com/files/music/flac/)

## Reverse Engineering
- [Peganza Pascal Analyzer](https://www.peganza.com/)
- [A Deep Dive into the Turbo Pascal Compiled Code](https://github.com/daelsepara/turbo-pascal-assembly)
- [Awesome Pascal](https://github.com/Fr0sT-Brutal/awesome-pascal)
- [TDInfo Parser for IDA](https://github.com/ramikg/tdinfo-parser)
- [Duncan Murdoch's Programs](https://www.murdoch-sutherland.com/programs/index.htm)
- [Rebuild of Turbo Pascal exe missing TPU modules](https://comp.lang.pascal.borland.narkive.com/1B3WeJkX/rebuild-of-turbo-pascal-exe-missing-tpu-modules)
- [Reverse Engineering Delphi Binaries in Ghidra with Dhrake](https://blag.nullteilerfrei.de/2019/12/23/reverse-engineering-delphi-binaries-in-ghidra-with-dhrake/)
- [Hachoir is a Python library to view and edit a binary stream field by field](https://github.com/vstinner/hachoir)
- [Kaitai Struct: declarative language to generate binary data parsers](https://github.com/kaitai-io/kaitai_struct)

## Similiar Pascal Games

### [HROT](https://en.wikipedia.org/wiki/Hrot)
- [HROT Demo](https://www.gog.com/en/game/hrot_demo)
- [HROT CLI Tools](https://github.com/joshuaskelly/hrot-cli-tools)
```cpp
/* HROT .PAK FILE FORMAT */
namespace hrot::pak
{
struct header
{
    c8<4> magic = "HROT"
    u32   names;
    u32   count; // 128 is file count
};

struct entry
{
    c8<120> name; // terminated with 0x00
    u32 pos;
    u32 len;
};
};
```
