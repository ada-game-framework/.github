<!-- ## Hi there 👋 -->

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->

# Ada Game Framework (an organisation)

* [App stores and the GPL](#App-stores-and-the-GPL)
* [Positive Quotes](#Positive-Quotes)
  1. [John Carmack](#John-Carmack)
  2. [NVIDIA](#NVIDIA)
* [The Plan](#The-Plan)
* [Future Plans](#Future-Plans)
  1. [SDL3](#SDL3)
  2. [ShAda](#ShAda)
  3. [Demos](#Demos)
* [Sponsors](#Sponsors)

Note: Still working this stuff out.

I started SDLAda a fews after I left the games industry for good knowing that Ada was a better language for developing games. With SDLAda I think I've proven how a highly portable library and a highly portable type safe language could work together to make game development faster and easier.

The aim is to be able to download the bits you need to create a portable game easily using Alire to add in the dependencies and handle building, testing and eventually (hopefully) packaging.

## App stores and the GPL

Only non-GPL'd projects will be found here (LGPL maybe, possibly). The GPL causes issues in these places where I'd like to see these libraries used and therefore I won't allow any GPL'd library, especially GPL'd bindings, here. Only projects with permissive licences will be allowed here.

There will be bindings to commercial libraries, but these libraries will be useable on platforms with their specific commercial licences, trying to restrict their use by enforcing a binding with a more restrictive licence doesn't make sense.

Remember SDL2 was originally licensed under the GPL which changed back to ZLib when Valve got involved because they could see the issues.

We still need legal clarification of using the GNAT RTS (GPLv3 with linking exception) in these places. The GPL's IR clause is still an issue.

## Positive Quotes

### John Carmack

> I actually have thought about Ada; there is a lot of good there, but it has an undeservedly terrible reputation.
>
> https://nitter.net/notfonk/status/398091658937389056

This "reputation" was spread by people who hated the language before even seeing the final specification for it.

> I read the ada spec a decade ago,and I was very impressed — it was the butt of jokes about design by government committee, but it looked pretty good to me...
>
> https://nitter.net/ID_AA_Carmack/status/1094603510304395265#m

FYI, it was *never* designed by committee.

> It is interesting how hearing about Ada in the old days it was easy to jump to a mocking “Big government programming language! Ha!” position, but looked at later, most of the decisions look pretty sound.
>
> https://nitter.net/ID_AA_Carmack/status/1314729151040020480#m

Re: Doom in Ada…

> ADA would be just fine. COBOL wouldn’t be pleasant.
>
> https://nitter.net/ID_AA_Carmack/status/1202983386559610880#m

### NVIDIA

>  “What if we just stopped using C?”
>
> [NVIDIA: Adoption of SPARK Ushers in a New Era in Security-Critical Software Development](https://www.adacore.com/papers/nvidia-adoption-of-spark-new-era-in-security-critical-software-development)

NVIDIA have been developing their new Ada Lovelace GPU firmware with the Ada / Spark languages.

## The Plan

The plan is to provide a set of Ada libraries which will enable someone or a company to create a game and/or game engine based on top of said libraries, these could be bindings or ports.

There will be overlap between projects as there are for any programming language and you can choose whichever you want to use.

You can imagine the set of libs as follows:

```bash
                             Your game
-----------------------------------------------------------------------
                               Other
                                 |
                    +--------+---+----+---------+
                    |        |        |         |
                   KTX*   Spine*    Tiled    AssImp*


                             Physics
                                |
                      +---------+--------+
                      |         |        |
                  Chipmunk*   Box2D+   Bullet+


                 Networking                     Platform Integration
                     |                                   |
            +--------+-------+                      +----+----+
            |                |                      |         |
         SDL_Net*   GameNetworkingSockets*     Steamworks*    ?


                GUI                                          Audio
                 |                                             |
      +----------+------------+-----------+            +-------+--------+
      |          |            |           |            |       |        |
   cimGUI+    Nuklear*   Ultralight*  NoesisGUI*     FMOD*   Wwise*   OpenAL


                          Graphics                       Video
                             |                             |
            +----------+-----+----+---------+          +---+
            |          |          |         |          |
          OpenGL*   Vulkan*     Metal*    DX3D*     libavif*


                               Maths*
-----------------------------------------------------------------------
                       Base libs, i.e. SDL, ASFML

```

\* My own projects, once I get moved, I will set up [Github sponsors](https://github.com/sponsors/Lucretia) on my profile so if anyone would like to sponsor the work, they can.

\+ Projects which (might) need to be patched to work with SDLAda.

### Maths

I have an old library I wrote about 20 years ago after coming out of the games industry, it was developed for OpenGL, but I am going to reuse/rewrite it to create a fast/optimised library to base everything on.

I intend for this to use SIMD machine instructions where appropriate.

#### OpenGL

Back around the time I was developing the [NeHe](https://github.com/Lucretia/old_nehe_ada95) ports, I was developing a binding generator for OpenGL, this was never completed.

### ImgGUI

There exists a binding to [this](https://github.com/michael-hardeman/ImGui-Ada) lib which seems to be a fork of an unmaintained binding.

### Afmod

I chose to do this one first as there is a C API which can be bound a bit more easily, plus it's a smaller, although still large, API compared to Wwise. Another reason is that they now provide a Linux client and Wwise don't.

[X] Thin bindings

### Box2d / Bullet

* Charlie5 has bindings and ports of [Box2D](https://github.com/charlie5/Ada_Box2d) and bullet ongoing.

### OpenAL

* [darkestkhan](https://github.com/darkestkhan/oto) has a binding which seems to be for OpenAL-soft, I don't know why he named it Oto.
    * There is no Alire crate for this yet.

### Tiled

* Fabien Chouteau from AdaCore has a [Tiled](https://github.com/Fabien-Chouteau/tiled-code-gen) lib which I haven't checked out yet. I'm not sure if this is going to be everything required for a Tiled runtime.
* His binding uses XMLAda which is way too heavy for games, so I think we can cross this off.

### Networking

* I really don't know much about networking, so not sure what to do here. I know there ie enet, yojimbo and now just found out of about Valve's [GameNetworkingSockets](https://github.com/ValveSoftware/GameNetworkingSockets).

### Platforms yet to work or be tested

* iOS
* Android
* WinRT (UWP)
  * Alex Gamper has a [runtime](https://github.com/Alex-Gamper/Ada-WinRT-Runtime/) and an [API](https://github.com/Alex-Gamper/Ada-WinRT). The latter is LGPLv3, which should be fine on Windows Store as that is the only place this library would be use.
    * There are no Alire crates for them yet.

## Future Plans

### SDL3

The way I have written the bindings to SDL2 should make the transition to SDL3 pretty easy as a lot of the changes in SDL3 are changes to names to make them more consistent and readable, which I already did in the bindings.

Ryan also rewrote the SDL_Net library for SDL3 as he wasn't happy with it.

#### ShAda

I thought about this about 10 years ago and now with SDL3 it kind of makes sense to do it. A platform independent Ada based shader language which compiles to SDL3's shader bitcode.

### Demos

There should be demonstration programs / games which show how to actually use the various libraries published here.

## Sponsors

Your company logo / profile here.
