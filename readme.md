### Temp Set-up | shell.nix ###
for now make sure to run cargo w/ 'nix-shell --run "cargo run"'
> will add to flake.nix later as a mkShell / devShell

5/5 Bevy 0.12 Tutorial Series 
| https://www.youtube.com/playlist?list=PL2wAo2qwCxGDp9fzBOTy_kpUTSwM1iWWd

### All Schedules in Main ###
Once on Start-up:
* [PreStartup]
* [Startup]
* [PostStartup]
///
Run Every Frame:
* ['First']
* ['PreUpdate']
* ['StateTransition']
* ['RunFixedUpdateLoop']
///
* ['FixedUpdate'] 0 - infinite times; dependent on time elapsed | runs after fixed period of time | like for physics
///
* ['Update']
* ['PostUpdate']
* ['Last']

Should only really StartUp/PostStartup & FixedUpdate/Update Schedules
; For Basic Use | Like my Use Case ;
+ if adding; use SystemSets +

can explicity order systems using .before() & .after()
> specify dependencies

.chain() can allow ordering multiple systems in sequence
[sequential execution via order defined; like in a tuple]

flush points are moments in execution where Bevy applies all pending changes
entity creation / component insertion / despawning entities
these happen between schedules:

First || Flush || PreUpdate || Flush || Update || Flush || PostUpdate || Flush

most relevant / important one for most part is the flush between Update & PostUpdate
[could be less confusing over time; flushpoints may be applied automatically in future]

apply_deferred systems can be included as a built-in
> can insert a flushpoint into key areas

SystemSets allow us to group systems into sets and define their order relative to each other
> more scalable for groupings of systems
