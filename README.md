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
#ifdef __cpluplus
extern "C" {
#include <cstdint>
#include <cstddef>
#include <cstdlib>
#include <cstdio>
#else
#include <stdint.h>
#include <stddef.h>
#include <stdlib.h>
#include <stdio.h>
#endif
#include <sys/stat.h>

typedef uint32_t u32;
typedef  int32_t i32;
typedef uint16_t u16;
typedef  int16_t i16;
typedef uint8_t   u8;
typedef uint8_t   i8;
typedef float    f32;

#pragma pack(push,1)
typedef struct {
    uint16_t vi[4];
    uint16_t uv[4][2];
    uint16_t next;
    uint16_t distant;
    uint8_t  group;
    uint8_t  flags;
    uint16_t uv_off;
} face;

typedef struct {
union
{
    struct { i16 x,y,z; };
    i16 xyz[3];
};
} i16x3;

typedef struct {
union
{
        struct { i16 x,y; };
        i16 xy[2];
};
} i16x2;

typedef struct {
        struct animap {
                u16 model[20];
                u16 sub_model[6][2];
        } anims;
        struct gsnd {
                u16 id[3];
        } gsnd;
        struct sfx {
                u16 len[8];
                u16 vol[8];
        } sfx;
        face   faces[400];
        i16x3  overt[256];
        i16x3  rvert[256];
        i16x3 shvert[256];
        i16x2 scvert[256];
        u16        vcount;
        u16        fcount;
        u16            th;
} car_header;

typedef struct
{
        face   faces[400];
        i16x3  overt[256];
        i16x3  rvert[256];
        i16x3 shvert[256];
        i16x2 scvert[256];
        u16        vcount;
        u16        fcount;
        u16            th;
} c3o_header;
#pragma pack(pop,1)

enum format
{
        CHASM_FORMAT_NONE = 0 << 0,
        CHASM_FORMAT_3O   = 1 << 0,
        CHASM_FORMAT_CAR  = CHASM_FORMAT_3O + 1 << 1,
};

/* .car Chasm: The Rift 3D model file format frame count */ 
size_t csm_model_car_frame_count(car_header* hdr)
{
        size_t dst = 0;
        for(size_t i = 0; i < 20; i++)
                dst += hdr->anims.model[i];
        for(size_t i = 0; i < 6; i++)
        {
                const size_t sum = hdr->anims.sub_model[i][0] + hdr->anims.sub_model[i][1];
                dst += sum == 0 ? 0 : sum + sizeof(c3o_header);
        }
        return dst;
}

/* .car Chasm: The Rift 3D model file format frame sfx length */ 
size_t csm_model_car_sfx_len(car_header* hdr)
{
        size_t dst = 0;
        for(size_t i = 0; i < 8; i++)
                dst += hdr->sfx.len[i];
        return dst;
}

/* .3o/.car Chasm: The Rift 3D model file format identifaction */
enum format csm_model_format(uint8_t* buf, size_t len)
{
        size_t       hdr_len = sizeof(c3o_header);
        const size_t car_len = sizeof(car_header) - hdr_len;
        size_t            tw = 64;
        c3o_header*      c3o = (c3o_header*)buf;
        car_header*      car = (car_header*)buf;

        if(buf != NULL && len > 0)
        {
                if(hdr_len  + c3o->th * tw == len)
                        return CHASM_FORMAT_3O;

                hdr_len += car_len;
                tw       = csm_model_car_frame_count(car) + csm_model_car_sfx_len(car);

                if(hdr_len + car->th + tw == len)
                        return CHASM_FORMAT_CAR;
        }
        return CHASM_FORMAT_NONE;
}
#ifdef __cplusplus
};
#endif
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
