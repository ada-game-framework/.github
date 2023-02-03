## Hi there 👋

<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->

# Ada Game Development (an organisation)

I've set up this organisation to allow others to more easily work on SDLAda and to organise other game development specific libs for Ada in one place.

Only non-GPL'd projects will be found here (LGPL maybe a possibility), the GPL causes issues in some places where I'd like to see these libraries used, App Stores, and therefore I won't allow them here. This does not mean that some of these libs won't bind to commercial libraries, they will, but these libraries will be useable on platforms with their commercial licences.

We still need legal clarification of using the GNAT RTS (GPLv3 with linking exception) in these places. The GPL's IR clause is still an issue.

Note: Still working this stuff out.

## The Plan

The plan is to provide a set of Ada libraries which will enable someone or a company to create a game and/or game engine based on top of said libraries, these could be bindings or ports.

You imagine the set of libs as being like this:

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
                      +---------+---------+
                      |         |         |
                   Chipmunk*  Box2D    Bullet


               Networking    Platform Integration
                   |                    |
                   +               +----+----+
                   |               |         |
                   ?         Steamworks*    ?


                GUI                                 Audio
                 |                                    |
      +----------+------------+               +-------+--------+
      |          |            |               |       |        |
   cimGUI*   Ultralight*  NoesisGUI*        FMOD*   Wwise*  OpenAL


                                Graphics
                                   |
                  +----------+-----+----+---------+
                  |          |          |         |
               OpenGL*    Vulkan*    Metal*    DX3D*


                               Maths*
-----------------------------------------------------------------------
                       Base libs, i.e. SDL, ASFML

```

All the above labelled with an asterisk are my own projects, once I get moved, I will set up [Github sponsors](https://github.com/sponsors/Lucretia) on my profile so if anyone would like to sponsor the work, they can.

### Maths

I have an old library I wrote about 20 years ago after coming out of the games industry, it was developed for OpenGL, but I am going to reuse/rewrite it to create a fast/optimised library to base everything on.

I intend for this to use SIMD machine instructions where appropriate.

#### OpenGL

Back around the time I was developing the [NeHe](https://github.com/Lucretia/old_nehe_ada95) ports, I was developing a binding generator for OpenGL, this was never completed.

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

### Networking

* I really don't know much about networking, so not sure what to do here. I know there ie enet, yojimbo and now just found out of about Valve's [GameNetworkingSockets](https://github.com/ValveSoftware/GameNetworkingSockets).

### Platforms yet to work or be tested

* iOS
* Android
* WinRT (UWP)
  * Alex Gamper has a [runtime](https://github.com/Alex-Gamper/Ada-WinRT-Runtime/) and an [API](https://github.com/Alex-Gamper/Ada-WinRT). The latter is LGPLv3, which should be fine on Windows Store as that is the only place this library would be use.
    * There are no Alire crates for them yet.
