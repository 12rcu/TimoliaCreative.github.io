# Dungeon Rush

Dungeon Rush is a standalone plugin that can generically execute commands in
minecraft designed to procedurally generate/build rooms together.

## Concept

![DR_Concept.png](../_media/dr/DR_DOC.png)

## Usage

To initialize a dungeon rush project call within the addon:

````kotlin
val config = DRConfig(
    roomBatchSize = 7..10, 
    initialPos = Triple(0, 100, 0)
)

dungeonRush(config) {
    room {}
}
````

### Config

The `roomBatchSize` is to determine how many rooms are spawned till an end room
will be spawned. Dungeon Rush will randomly select a value from that range.

### Rooms

After defining the config you can add as many rooms as you wish.

````kotlin
dungeonRush(config) {
    room {
        size = Triple(20, 10, 40)

        buildCommands = arrayListOf(DRCommand.unsafe("/say building ..."))
        buildTime = 10.2f
        commandsAfterBuild = arrayListOf(DRCommand.unsafe("/say finished building"))

        tags = arrayListOf("cave")
        nextRoomReqTags = arrayListOf("cave")
        nextRoomForbiddenTags = arrayListOf("water")
    }
}
````


**Build Command Requirements:**

- a player needs to be in range of a structure if it needs to be build

### Special Tags:

- `END` the end tag indicates that this room will only be used as the last room of a batch, at least 1 is required
- `BEGIN` this room will only be used as the start of a room batch, at least 1 is required
- `Exit:Forward` this tag indicates that the next room will be generated in the current direction
- `Exit:Right` this tag indicates that the next room will be generated in the right direction
- `Exit:Left` this tag indicates that the next room will be generated in the left direction
- `LEFT` indicates the current rotation, do not use
- `RIGHT` indicates the current rotation, do not use
- `FORWARD` indicates the current rotation, do not use
