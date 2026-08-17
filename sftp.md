# SFTP file transfers

Splinter’s SSH protections may throttle workloads that open many SFTP connections in parallel. This is expected behaviour rather than a fault: the limits help protect the server against connection-based DoS attacks, and we are not currently planning to relax them.

If transferring many files:

* Best: Configure your SFTP client (e.g. FileZilla) to use a single persistent connection rather than many parallel connections.
* Workaround: archive/zip many small files and transfer the archive as a single file.
* SFTP Alternative: try `rsync` over SSH or `scp`

Standard SFTP transfers over a small number of connections should work normally.
