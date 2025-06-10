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
- [noesis_py still misses .3O/.CAR support](https://github.com/atrzaska/noesis_py)
- [P3DO Explorer/Organizer](www.senosoft.com/softp3doDownload.php)
- [c3d](https://github.com/pyushkevich/c3d)
- [daz3d](https://github.com/daz3d/)
- [Carrara](https://www.daz3d.com/carrara-8-5-pro)

```cpp
/* QUAD/TRIANGLE polygon face */
struct face
{
        vec::u16 <               4>              indices;
        arr::type<vec::u16<2>,   4>                   uv;
        sca::i16                                    next;
        sca::i16                                 distant;
        sca::u8                                      num;
        sca::u8                                    flags;
        sca::u16                              sprite_off;
};

/* .CAR Chasm: The Rift Carrara 3D model file format 
struct car
{
        arr::type<sca::u16   ,  20>           animations;
        arr::type<vec::u16<2>,   3> submodels_animations;
        arr::type<sca::u16   ,   6>             unknown0;
        arr::type<sca::u16   ,   3>               sounds;
        arr::type<sca::u16   ,  16>                  sfx;

        arr::type<face       , 400>                faces; // 0x0066
        arr::type<vec::i16<3>, 256>                overt; // 0x3266
        arr::type<vec::i16<3>, 256>                rvert;
        arr::type<vec::i16<3>, 256>               shvert;
        arr::type<vec::i16<2>, 256>               scvert;

        sca::u16                            vertex_count; // 0x4866
        sca::u16                              face_count; // 0x4868
        sca::u16                                      th; // 0x486A filesize = th * 64;

        size_t sounds_offset()
        {
                size_t dst = th + 0x486Cu;
                for(size_t i = 0; i < 20; i++) dst += animations[i];
                for(size_t i = 0; i < 3u; i++) dst += submodels_animations[i].sum() + 04806u;
                return dst;
        }
};
```

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
