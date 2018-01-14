# TODO

It is really the first commands I would often use, and easy to extend. That's nice.   
But things that seem to need improvement....


It's unfortunate that this runs in client-side python, instead of transferring & running some statically linked binary.
(I.e. pushing it into a fd via ssh and executing right from there)
There are a lot of cases where the remote end will not be able to execute run stuff stored locally at all.   
We need to check that fossor is able to reliably detect when it has encountered a situation where it failed to complete, and that it is able to tell us so.
We should also harden it as much as possible (use available ramdisks, etc) so it will be able to complete in most edge cases.

But - it makes sense to put it in place long before the hardening is finished.
Just need to make sure there's a throttle on how often it can be run at all (incident storms, stuck on stale commands, etc)



## Unify with what comes before and after

* Make sure there's a connection handler that uses the same interface/format for saying "i was unable to run fossor"
* Make sure it can also say "I was able to run anything that is part of fossor"
* Make sure it will not end up with 4000 stuck processes on the target host.
* Make the results are really evaluated, summarized and stored (will see after testing)
* Make sure the persistent storage of the results is ready to be merged with other results not from fossor.

## Hardening

__Make sure this can run on a system that is not OK__   
That's the whole point, right?

* Should run if disk is full
* Should run if /tmp is not writable
* Should run if disk is not writable
* Should add a check that understands no-fork-possible situations (no ram, pid counter exhausted, slow pid allocation)
* Should detect if run aborted in a global, not singular bit
* Should run if /opt is corrupted (errors might or not be in dmesg, but mostly IO will stall, and if they got the tests in /opt it WILL be affected)
* Should run if dmesg has oddities (being empty, for most)
* Should not choke if someone logs iptables stuff to cons
* Should never display an outdated result from a prior run
* Should report something even if it can't run the plugins at all (chmod 000 /opt/.../plugins...)

## Safeties

* Should clean up after itself
* Should handle errors in cleanup
