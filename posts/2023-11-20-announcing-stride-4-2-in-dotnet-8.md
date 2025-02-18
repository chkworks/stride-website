---
title: 'Announcing Stride 4.2'
author: vaclav
popular: true
tags: ['4.2','Release']
---

Stride contributors are thrilled to announce the release of Stride 4.2, now fully compatible with .NET 8 and leveraging the latest enhancements in C# 12. This release brings significant improvements in performance, stability, and developer experience.

---

Table of Contents:

[[TOC]]

A massive thank you to the open-source Stride community for your dedicated contributions. This release saw X contributions from over Y amazing contributors, each playing a crucial role in making Stride 4.2 a reality.

## Download and Upgrade

You can [download the Stride 4.2 Installer](https://www.stride3d.net/download/) today. Release notes are available [here](https://doc.stride3d.net/latest/en/ReleaseNotes/ReleaseNotes.html).


## What's new in Stride 4.2
Stride 4.2 includes numerous enhancements and improvements.

- **[.NET 8 Integration](https://devblogs.microsoft.com/dotnet/announcing-dotnet-8/)**: Experience the power and efficiency of the latest .NET version in your game development. 
  - Full compatibility with .NET 8, taking advantage of [improved runtime performance](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-8/)
  - **[C# 12 features](https://devblogs.microsoft.com/dotnet/announcing-csharp-12/)**: Utilize cutting-edge language features to write more concise and maintainable code, enhancing coding efficiency and reducing boilerplate code
- **[Changed Assimp binding to Silk.Net.Assimp](https://github.com/stride3d/stride/pull/1158)**
  - This change allows us to remove much of the C++/CLR code used by the asset compiler and brings us one step closer to running the asset compiler on non-windows systems.
- [Migration NET6+ and more gettextnet#2](https://github.com/stride3d/gettextnet/pull/2)
  - Updated all of gettext.NET to the latest stable version of NET
- [Enable multiple profiler consumers and add a timeline/tracing profiler #1788](https://github.com/stride3d/stride/pull/1788)
  - This feature adds a profiler outputting data in chrome://tracing format and changes Profiler to make that possible.
- [Feature: Add Support for F# and VB Project Types #1821](https://github.com/stride3d/stride/pull/1821)
  - Currently only for code-only projects
    - [F# examples](https://stride3d.github.io/stride-community-toolkit/manual/code-only/examples/basic-examples-fs.html)
    - [Visual Basic examples](https://stride3d.github.io/stride-community-toolkit/manual/code-only/examples/basic-examples-vb.html)
- [Stride Diagnostics Analyzer #1864](https://github.com/stride3d/stride/pull/1864)
  - Implements a code analyzer to show helpful warnings in your IDE and at compilation when any of your members or structures are incompatible with the serialization system.
- [OpenVR Handle custom resolution specified by the user through VR settings #2000](https://github.com/stride3d/stride/pull/2000)
- [Editor - Add dynamic snapping for selected objects #1801](https://github.com/stride3d/stride/pull/1801)
  - Implements a dynamic snapping used while holding down a key (default: Left Shift) on manipulating (rotating/moving/scaling) an object/entity. 
  - Adds a new Hotkey Setting for dynamic snapping
  - Adds a Method to handle dynamic snapping
- [Editor - Let the user pick which animation stack to import in an fbx #1977](https://github.com/stride3d/stride/pull/1977)
  - This change introduces a field that users can edit to control which animation the engine should import from the source FBX.
- [Editor - Added the ability to copy imported assets automatically to the Resources dir #1827](https://github.com/stride3d/stride/pull/1827)
  - We recommend storing assets within your project's resource directory to avoid issues that may arise when sharing the project or moving files around.
  - Whenever users import assets that are located outside of the resource directory, they will now be presented with a dialog box asking them whether the file should be copied to that directory.

## Stride 4.2 Feature Overview

### F# and Visual Basic Integration

A pivotal PR has enabled **F#** and **Visual Basic** support for game development in Stride. This feature is currently limited to a code-only approach. Detailed insights and tutorials will be provided in upcoming blog posts.

We will use the [Stride Community Toolkit [WIP]](https://stride3d.github.io/stride-community-toolkit/), with further details to be covered in a separate post.

Below is a simple example of rendering a capsule using F#:

```fsharp
open Stride.CommunityToolkit.Engine;
open Stride.CommunityToolkit.ProceduralModels;
open Stride.Core.Mathematics;
open Stride.Engine;

let game = new Game()

let Start rootScene =
    game.SetupBase3DScene()
    game.AddProfiler() |> ignore

    let firstBox = game.CreatePrimitive(PrimitiveModelType.Capsule);
    firstBox.Transform.Position <- new Vector3(0f, 2.5f, 0f)
    firstBox.Scene <- rootScene

[<EntryPoint>]
let main argv =
    game.Run(start = Start)
    0
```

{% img 'Example basic 3d scene with a capsule' '/images/blog/2023-11/stride-game-engine-example01-basic-3d-scene.webp' %}

The equivalent Visual Basic example:

```vb
Imports Stride.CommunityToolkit.Engine
Imports Stride.CommunityToolkit.ProceduralModels
Imports Stride.Core.Mathematics
Imports Stride.Engine

Module Program
    Private game As New Game()

    Sub Main()
        GameExtensions.Run(game, Nothing, AddressOf StartGame)
    End Sub

    Private Sub StartGame(rootScene As Scene)
        game.SetupBase3DScene()
        game.AddProfiler()

        Dim entity = game.CreatePrimitive(PrimitiveModelType.Capsule)
        entity.Transform.Position = New Vector3(0, 8, 0)
        entity.Scene = rootScene
    End Sub
End Module

```

These examples showcase how F# and Visual Basic can be utilized in Stride. The Stride Community Toolkit provides a set of helpers and extensions designed to enhance your experience with the Stride Game Engine.

## Fixes
Although there have been [many fixes](**https://github.com/stride3d/stride/pulls?page=2&q=is%3Apr+merged%3A%3E2023-10-10**), we like to point out some of them out
- [Runtime rasterized fonts are broken #1750](https://github.com/stride3d/stride/issues/1750)
- [Game Studio doesnt reload sub projects after changes #1703](https://github.com/stride3d/stride/issues/1703)
- [Changing the comparison project related and not UPath related #1704](https://github.com/stride3d/stride/pull/1704)
- [Translations fix #1717](https://github.com/stride3d/stride/pull/1717)
- [C# Beginner Tutorial Build Errors #1652](https://github.com/stride3d/stride/issues/1652)
- [Can not create "C# Beginner" project #1650](https://github.com/stride3d/stride/issues/1650)

## Also good to know
Although not directly tied to Release 4.2, we have made some other big changes. For instance to our website and documentation. We also had another community meeting to address all those new members.
- [Website and documentation revamped and build process updated](https://www.stride3d.net/blog/announcing-website-update/)
- [Contributor section moved to docs](https://doc.stride3d.net/latest/en/contributors/ways-to-contribute.html)
- [Community meeting October 2023](https://www.stride3d.net/blog/community-meeting-october-2023/)


## Links
- GitHub: [{{site.links.github-stride-url}}]({{site.links.github-stride-url}})
- Website: [{{site.links.stride-url}}]({{site.links.stride-url}})
- Documentation: [{{site.links.docs-manual-url}}]({{site.links.docs-manual-url}})
- Twitter: [{{site.links.twitter-url}}]({{site.links.twitter-url}})
- YouTube: [{{site.links.youtube-url}}]({{site.links.youtube-url}})


## Acknowledgements
We extend our heartfelt gratitude for all the hard work and donations that have been made. Your generous contributions significantly aid in the continuous development and enhancement of the Stride community and projects. Thank you for your support and belief in our collective efforts.

In particular we want to thanks these donors:

### Long time Stride supporters
*  {% include sponsor-org.md key:'vvvv' emoji:'🥇' %}

   <a href="https://visualprogramming.net/"><img src="https://images.opencollective.com/vvvv/8ab0acd/logo/256.png?height=72" alt="vvvv. A visual live-programming environment that takes you from rapid prototyping to final production"></a>

### Platinum Striders
* {% include sponsor-org.md key:'happenstance' emoji:'🏆' %}

  <a href="http://www.happenstancegames.com/"><img width=64 src="https://www.stride3d.net/images/sponsors/HappenLogo.webp" alt="Happenstance games logo"></a>

### Gold Striders

* {% include sponsor-user.md key:'vaclav' emoji:'🥇' %}
* {% include sponsor-org.md key:'lucid' emoji:'🥇' %}
* {% include sponsor-user.md key:'skidvis' emoji:'🥇' %}

This article was co-authored by [Aggror Jorn](https://github.com/Aggror).