# AwesomeChasm
Chasm: The Rift PC game resource collection.

## Ports
- [Chasm-Reverse Panzerchasm](https://github.com/Panzerschrek/Chasm-Reverse)
- [OpenChasm](https://github.com/alexey-lysiuk/OpenChasm)
- [Chasm: The Rift Portable Staging](https://www.moddb.com/games/chasm-the-rift/downloads/chasm-portable-staging)
- [Chasm: The Rift Demo](https://www.gog.com/en/game/chasmtherift_demo)
- [Zrift Chasm in Doom - Legacy Edition](https://www.moddb.com/mods/zrift-chasm-in-doom-legacy-edition/downloads/zrift-chasm-in-doom-legacy-edition-v11)

## Modding
- [Chasm: The Rift Archive](https://www.chasm3d.com/)
- [Shikadi Modding Wiki](https://moddingwiki.shikadi.net/wiki/Chasm:_The_Rift)
- [The Shadow Zone](https://discord.com/channels/768103789411434586/1374778669612007527)
  - [Chasm Modding Toolkit Package](https://discord.com/channels/768103789411434586/1374842906002718803)
  - [OpenSesame](https://discord.com/channels/768103789411434586/1374929171263918080)
- [moddb](https://www.moddb.com/games/chasm-the-rift)
- [Chasm: The Rift Pack](https://steamcommunity.com/sharedfiles/filedetails/?id=3128742113)
- [Chasm: The Rift - 3OVIEW.EXE DOS model viewer](https://www.chasm3d.com/files/dump/CDEMOf.zip)
- [Autodesk Animator](https://github.com/AnimatorPro)
- [Noesis .3O/.CAR 3D model viewer/converter](https://richwhitehouse.com/index.php?content=inc_stream.php)

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

/* .CAR Chasm: The Rift Caracter 3D model file format header */ 
struct CARHeader
{
    struct AniMap {
        arr::type<sca::u16   ,  20>                model; /* anim data sizes */
        arr::type<vec::u16<2>,   6>            sub_model; /* sub model anim data sizes */
    } anims;
    struct GSND {
        arr::type<sca::u16   ,   3>                   id; /* FallSound id */
    } gsnd;
    struct SFX {
        vec::u16<                8>                  len;
        vec::u16<                8>                  vol;
    } sfx;
};

/* .3O Chasm: The Rift 3D model file format */
struct c3o
{
        arr::type<face       , 400>                faces; // 0x0000
        arr::type<vec::i16<3>, 256>                overt; // 0x3200
        arr::type<vec::i16<3>, 256>                rvert;
        arr::type<vec::i16<3>, 256>               shvert;
        arr::type<vec::i16<2>, 256>               scvert;

        sca::u16                            vertex_count; // 0x4800
        sca::u16                              face_count; // 0x4802
        sca::u16                                      th; // 0x4804
};

/* .CAR Chasm: The Rift Caracter 3D model file format */ 
struct car : CARHeader, c3o
{
        size_t sounds_offset()
        {
                size_t dst = th + sizeof(struct car_header) + 0x4806u;
                for(size_t i = 0; i < 20; i++) dst += anims[i];
                for(size_t i = 0; i < 3u; i++)
                {
                        const size_t sum = sub_anims[i].sum();
                        dst += sum == 0 ? 0 : sum + 0x4806u;
                }
                return dst;
        }
        bool verify_length(const size_t len)
        {
            size_t acc = sounds_offset();
            for(size_t i = 0; i < sfx_len.size(); i++)
                acc += sfx_len[i];
            return acc == len;
        }
        bool set_sound(const size_t monster_number)
        {
            const size_t monster_index = monster_number - 100;
            if(monster_index >= 23)
                return false;

            for (size_t i = 0; i < gsnd.size(); ++i)
                SepPartInfo[monster_index + i].FallSound = gsnd[i];
            return true;
        }
};
```

## Music
- [Chasm: The Rift - FLAC OST music](https://www.chasm3d.com/files/music/flac/)

## Links
- [Chasm: The Rift - Website Recreation by Effektus](http://chasm.atspace.eu/)

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
## Similiar C++ Games

### [Perilous Warp](https://crystice.com/perilous-warp/)
