FS Listener
===========

Derived work from [synrc/fs](https://github.com/synrc/fs). 

There are 2 issues in initial `fs` design:

* impossible to change subscribed path after start of application, which makes it impossible 
to start `fs` as dependency and change the path to something else, as `cwd`
* impossible to start more, than one listener to changes

Initial issues: [syncr/fs#12](https://github.com/synrc/fs/issues/12), [syncr/fs#18](https://github.com/synrc/fs/pull/18)

Until this issues are unsolved for a long time in original repository, this derived 
work exists, and will be maintained to incorporate all upcoming features/bug fixes from
original `fs` implementation.

Backends
--------

* Mac [fsevent](https://github.com/thibaudgg/rb-fsevent)
* Linux [inotify](https://github.com/rvoicilas/inotify-tools/wiki)
* Windows [inotify-win](https://github.com/thekid/inotify-win)

NOTE: On Linux you need to install inotify-tools.

### Subscribe to Notifications

```erlang
> fs:start_link(fs_watcher, "/Users/5HT/synrc/fs"). % need to start the fs watcher
> fs:subscribe(fs_watcher). % the pid will receive events as messages
> flush(). 
Shell got {<0.47.0>,
           {fs,file_event},
           {"/Users/5HT/synrc/fs/src/README.md",[closed,modified]}}
```

### List Events from Backend

```erlang
> fs:known_events(fs_watcher). % returns events known by your current backend
[mustscansubdirs,userdropped,kerneldropped,eventidswrapped,
 historydone,rootchanged,mount,unmount,created,removed,
 inodemetamod,renamed,modified,finderinfomod,changeowner,
 xattrmod,isfile,isdir,issymlink,ownevent]
```

### Sample Subscriber

```erlang
> fs:start_logger(). % starts a sample process that logs events with error_logger
=INFO REPORT==== 28-Aug-2013::19:36:26 ===
file_event: "/tank/proger/erlfsmon/src/4913" [closed,modified]
```

Credits
-------

* Vladimir Kirillov
* Maxim Sokhatsky

OM A HUM
