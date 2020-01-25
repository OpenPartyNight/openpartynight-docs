# Overview of System Configuration

An OpenPartyNight system will store all its content under `/opt/openpartynight` as follows:

- `bin/` - Command scripts for launching the GUI, games and any other OpenPartyNight applications goes here
- `content/` - This is a samba share for storing game content, broken down for each game type that has compatible content
    - `content/dance/` - Content for dancing games (StepMania, ITG, etc) will be installed here and linked into the various game installation directories to reduce storage usage
    - `content/play/` - Content for other rhythm games (Frets on Fire, etc) will be installed here and linked into the various game installation directiores to reduce storage usage
    - `content/sing/` - Content for singing games (UltraStar Deluxe, Vocaluxe, etc) will be installed here and linked into the various game installation directories to reduce storage usage
- `games/` - This is where games are installed
- `store/` - This directory contains the installation profiles for the various games available through the OpenPartyNight store
- `system/` - OpenPartyNight GUI code and various system-level stuff goes in here, not to be touched unless you **seriously know what you're doing and are happy to break things**

Note: This directory structure is pre-emptive of OpenPartyNight development and may be subject to change.
