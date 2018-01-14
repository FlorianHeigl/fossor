# TODO

It's unfortunate that this runs in client-side python
It is really the first commands I would often use, and easy to extend

Some things that seem to need improvement


# Unify with what comes before and after

* Make sure there's a connection handler that uses the same interface/format for saying "i was unable to run fossor"
* Make sure it can also say "I was able to run anything that is part of fossor"
* Make the results are really evaluated, summarized and stored (will see after testing)
* Make sure the persistent storage of the results is ready to be merged with other results not from fossor.

# Hardening

Make sure this can run on a system that isn't OK   
That's the whole point, right?

* Should run if disk is full
* Should run if /tmp is not writable
* Should run if disk is not writable
* Should add a check that understands no-fork-possible situations (no ram, pid counter exhausted, slow pid allocation)
* Should detect if run aborted in a global, not singular bit
* Should run if /opt is corrupted (errors might or not be in dmesg)
* Should run if dmesg has oddities (being empty, for most)
* Should not choke if someone logs iptables stuff to cons
* Should never display an outdated result from a prior run

# Safeties

* Should clean up after itself
* Should handle errors in cleanup
