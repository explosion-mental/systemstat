# CPU load

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.cpu_load_aggregate() {
    Ok(cpu)=> {
        println!("Measuring CPU load...");
        thread::sleep(Duration::from_secs(1));
        let cpu = cpu.done().unwrap();
        println!("CPU load: {}% user, {}% nice, {}% system, {}% intr, {}% idle ",
                 cpu.user * 100.0, cpu.nice * 100.0, cpu.system * 100.0,
                 cpu.interrupt * 100.0, cpu.idle * 100.0);
    },
    Err(x) => println!("CPU load: error: {}", x)
}
```

# CPU temperature

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.cpu_temp() {
    Ok(cpu_temp) => println!("CPU temperature: {}", cpu_temp),
    Err(x) => println!("CPU temperature: {}", x)
}
```

# Load Average

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.load_average() {
    Ok(loadavg) => println!("Load average: {} {} {}", loadavg.one, loadavg.five, loadavg.fifteen),
    Err(x) => println!("Load average: error: {}", x)
}
```

# Memory info

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.memory() {
    Ok(mem) => println!("Memory: {} used / {} ({} bytes) total ({:?})",
                        saturating_sub_bytes(mem.total, mem.free),
                        mem.total, mem.total.as_u64(), mem.platform_memory),
    Err(x) => println!("Memory: error: {}", x)
}
```

# Boot Time

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.boot_time() {
    Ok(boot_time) => println!("Boot time: {}", boot_time),
    Err(x) => println!("Boot time: error: {}", x)
}
```

# Uptime

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.uptime() {
    Ok(uptime) => println!("Uptime: {:?}", uptime),
    Err(x) => println!("Uptime: error: {}", x)
}
```

# AC adapter status

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.on_ac_power() {
    Ok(power) => println!("AC adapter status: {}", power),
    Err(x) => println!("AC adapter status: error: {}", x)
}
```

# Battery life

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.battery_life() {
    Ok(bat) => print!("Battery: {}%, {}h{}m remaining",
                      bat.remaining_capacity * 100.0,
                      bat.remaining_time.as_secs() / 3600,
                      bat.remaining_time.as_secs() % 60),
    Err(x) => print!("Battery: error: {}", x)
}
```

# Swap

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.swap() {
    Ok(swap) => println!("Swap: {} used / {} ({} bytes) total ({:?})",
                         saturating_sub_bytes(swap.total, swap.free),
                         swap.total, swap.total.as_u64(), swap.platform_swap),
    Err(x) => println!("Swap: error: {}", x)
}
```

# Disk mounts

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.mounts() {
    Ok(mounts) => {
        println!("\nMounts:");
        for mount in mounts.iter() {
            println!("{} ---{}---> {} (available {} of {})",
                     mount.fs_mounted_from, mount.fs_type,
                     mount.fs_mounted_on, mount.avail, mount.total);
        }
    }
    Err(x) => println!("\nMounts: error: {}", x)
}

```

# Disk mount info

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.mount_at("/") {
    Ok(mount) => {
        println!("Mount at /:");
        println!("{} ---{}---> {} (available {} of {})",
                 mount.fs_mounted_from, mount.fs_type,
                 mount.fs_mounted_on, mount.avail, mount.total);
    }
    Err(x) => println!("\nMount at /: error: {}", x)
}
```

# Block device statistics

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.block_device_statistics() {
    Ok(stats) => {
        for blkstats in stats.values() {
            println!("{}: {:?}", blkstats.name, blkstats);
        }
    }
    Err(x) => println!("Block statistics error: {}", x)
}
```

# Network interfaces

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.networks() {
    Ok(netifs) => {
        println!("Networks:");
        for netif in netifs.values() {
            println!("{} ({:?})", netif.name, netif.addrs);
        }
    }
    Err(x) => println!("Networks: error: {}", x)
}
```

# Network traffic statistics

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.networks() {
    Ok(netifs) => {
        println!("Network interface statistics:");
        for netif in netifs.values() {
            println!("{} statistics: ({:?})", netif.name, sys.network_stats(&netif.name));
        }
    }
    Err(x) => println!("Networks: error: {}", x)
}
```

# Socket info

  --------- ------- --------- -------- ------- --------
  FreeBSD   Linux   OpenBSD   Window   MacOS   NetBSD
  ❌        ❌      ❌        ❌       ❌      ❌
  --------- ------- --------- -------- ------- --------

``` rust
let sys = System::new();
match sys.socket_stats() {
    Ok(stats) => println!("System socket statistics: {:?}", stats),
    Err(x) => println!("System socket statistics: error: {}", x)
}
```

\*
