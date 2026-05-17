Title: kvraft.pdf
Mapped Topic: Distributed systems labs and schedule
Source URL: https://pdos.csail.mit.edu/6.5840/figs/kvraft.pdf
Source Type: official_course
Trust Score: 97
Fetched At: 2026-04-17T07:00:46+00:00
Mapped From CSE.md Section: Part 1 / Part 2.E

# Content

rsm.go
raft.go
server.go
client.goargs
reply
1. Call Put/Get 8. Put/Get return
cmd
msg
3. Invoke Start(cmd) 4. Send command message
SnapshotValid=false
CommandValid=true
opreq
opres
5. Invoke DoOp(opreq)
6. DoOp return
req
res
2. Invoke Submit(req)
7. Submit return
(a) Flow of executing an operation
raft.go
rsm.go server.go
size
1. Invoke PersistBytes() and return
snap
2. Invoke Snapshot() and return
(snap,idx)
3. Invoke Snapshot(snap,idx)
(b) Flow of creating a snapshot
raft.go
rsm.go server.go
args
1. Receive InstallSnapshot
msg
2. Send snapshot message
SnapshotValid=true
CommandValid=false
snap
3. Invoke Restore(snap)
(c) Flow of receiving a snapshot
RPC call
Function invocation
Sending via applyCh
