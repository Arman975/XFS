[pratikj@localhost NewBcc]$ sudo ./27script.sh
[sudo] password for pratikj: 
Tracing "xfs_file_fsync"... Ctrl-C to end.
^C
Message from syslogd@localhost at Dec 27 19:12:37 ...
 kernel:NMI watchdog: BUG: soft lockup - CPU#1 stuck for 22s! [funcgraph:6910]
myjob: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=sync, iodepth=1
...
fio-3.7
Starting 4 processes
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.521 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.101 us    |      down_read();
 3)   0.411 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 144.727 us  |      xlog_cil_force_lsn [xfs]();
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.751 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.070 us    |      down_read();
 0)   0.291 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   0.531 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.141 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.301 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 26.240 us   |      xlog_state_release_iclog [xfs]();
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.030 us    |      filemap_check_errors();
 0)   0.250 us    |    }
 0)   0.080 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.060 us    |      down_read();
 0)   0.260 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   0.320 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.080 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.101 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 2)   0.481 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.060 us    |      down_read();
 2)   0.300 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.561 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.141 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6937   
 ------------------------------------------

 0) ! 13969.38 us |      }
 0) + 50.877 us   |      remove_wait_queue();
 0) ! 14198.43 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.100 us    |      up_read();
 0)   0.822 us    |    }
 0) ! 14203.50 us |  }
 1) ! 14124.09 us |      } /* schedule */
 1)   1.854 us    |      remove_wait_queue();
 1) ! 14134.79 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.111 us    |      up_read();
 1)   0.821 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6934   
 ------------------------------------------

 1) ! 14130.29 us |      } /* schedule */
 1)   0.330 us    |      remove_wait_queue();
 1) ! 14134.52 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.080 us    |      up_read();
 1)   0.691 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 14382.70 us |      }
 2)   0.641 us    |      remove_wait_queue();
 2) ! 14387.96 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.110 us    |      up_read();
 2)   0.822 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2) ! 8481.911 us |      blkdev_issue_flush();
 ------------------------------------------
 1)    fio-6934    =>    fio-6935   
 ------------------------------------------

 1) ! 5853.483 us |      }
 1) ! 5856.389 us |    }
 1) ! 19997.32 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6935    =>    fio-6934   
 ------------------------------------------

 1) ! 8504.444 us |      } /* blkdev_issue_flush */
 1) ! 8505.566 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 22644.61 us |  } /* xfs_file_fsync [xfs] */
 2) ! 8484.987 us |    }
 2) ! 22877.55 us |  }
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.401 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.331 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   0.621 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.220 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 277.891 us  |      xlog_state_release_iclog [xfs]();
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.541 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.380 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 314.560 us  |      xlog_cil_force_lsn [xfs]();
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 0)   0.100 us    |      _raw_spin_lock();
 2)   0.471 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 0)   0.190 us    |      add_wait_queue_exclusive();
 2)               |    xfs_ilock [xfs]() {
 2)   0.081 us    |      down_read();
 0)               |      schedule() {
 2)   0.311 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.541 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.111 us    |      add_wait_queue_exclusive();
 2) ! 10067.96 us |      schedule();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.120 us    |      filemap_check_errors();
 3)   0.491 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.331 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.521 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.160 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6935   
 ------------------------------------------

 1) ! 9994.795 us |      } /* schedule */
 1)   0.261 us    |      remove_wait_queue();
 1) ! 10314.17 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.040 us    |      up_read();
 1)   0.311 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 2)   0.251 us    |      remove_wait_queue();
 2) ! 10072.89 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.311 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 1) ! 9894.424 us |      } /* schedule */
 1)   0.130 us    |      remove_wait_queue();
 1) ! 9897.008 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.290 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 10100.91 us |      } /* schedule */
 1)   0.120 us    |      remove_wait_queue();
 1) ! 10383.78 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.260 us    |    }
 1) ! 10386.33 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6934    =>    fio-6935   
 ------------------------------------------

 3) ! 4022.031 us |      } /* blkdev_issue_flush */
 3) ! 4023.994 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 14341.91 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 6663.690 us |      } /* blkdev_issue_flush */
 1) ! 6665.463 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1)   ==========> |
 1)               |    smp_apic_timer_interrupt() {
 1)   0.151 us    |      irq_enter();
 1)   0.040 us    |      exit_idle();
 1) + 34.997 us   |      local_apic_timer_interrupt();
 1)   0.241 us    |      irq_exit();
 1) + 71.577 us   |    }
 1)   <========== |
 1) ! 16692.13 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6934    =>    fio-6936   
 ------------------------------------------

 1) ! 8873.208 us |      } /* blkdev_issue_flush */
 1) ! 8874.250 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 18950.04 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6936    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.761 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.090 us    |      down_read();
 1)   0.331 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 18.516 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.161 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.100 us    |      filemap_check_errors();
 3)   0.562 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.070 us    |      down_read();
 3)   0.311 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.882 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 ------------------------------------------
 1)    fio-6937    =>    fio-6936   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 3)   0.231 us    |      xlog_state_switch_iclogs [xfs]();
 1)               |    filemap_write_and_wait_range() {
 1)   0.031 us    |      filemap_check_errors();
 1)   0.261 us    |    }
 3) + 67.479 us   |      xlog_state_release_iclog [xfs]();
 1)   0.090 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.110 us    |      down_read();
 1) + 32.351 us   |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.591 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.251 us    |      _raw_spin_lock();
 3)   0.160 us    |      _raw_spin_lock();
 3)   0.260 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 1)   0.330 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.311 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.070 us    |      down_read();
 1)   0.310 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.541 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.090 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 13524.75 us |      }
 1) ! 294.903 us  |      remove_wait_queue();
 ------------------------------------------
 0)    fio-6937    =>    fio-6935   
 ------------------------------------------

 0) ! 13518.60 us |      }
 0)   8.546 us    |      remove_wait_queue();
 0) ! 13602.00 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.300 us    |    }
 0) ! 13605.87 us |  }
 1) ! 13843.18 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.040 us    |      up_read();
 1)   0.301 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 4318.443 us |      blkdev_issue_flush();
 2) ! 14293.63 us |      } /* schedule */
 2)   0.591 us    |      remove_wait_queue();
 2) ! 14337.54 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.120 us    |      up_read();
 2)   0.391 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2) ! 14299.12 us |      } /* schedule */
 2)   0.121 us    |      remove_wait_queue();
 2) ! 14301.61 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.030 us    |      up_read();
 2)   0.250 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.521 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.080 us    |      down_read();
 0)   0.330 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 18.966 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.221 us    |      xlog_state_switch_iclogs [xfs]();
 0) + 16.902 us   |      xlog_state_release_iclog [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.431 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 1) ! 4320.247 us |    }
 1) ! 18167.19 us |  }
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 7178.109 us |      }
 2) ! 7181.956 us |    }
 2) ! 21555.29 us |  }
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 9817.567 us |      } /* blkdev_issue_flush */
 0) ! 9819.220 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 24123.45 us |  }
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.972 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.080 us    |      down_read();
 1)   0.401 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) ! 140.514 us  |      xlog_cil_force_lsn [xfs]();
 1)   0.050 us    |      _raw_spin_lock();
 1)   0.170 us    |      add_wait_queue_exclusive();
 1) ! 3255.093 us |      schedule();
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 2)   0.451 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.080 us    |      down_read();
 2)   0.330 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.561 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.131 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.091 us    |      filemap_check_errors();
 0)   0.851 us    |    }
 0)   0.080 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.180 us    |      down_read();
 0)   0.721 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.272 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.070 us    |      _raw_spin_lock();
 0)   0.400 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3) ! 27205.06 us |      }
 3)   0.191 us    |      remove_wait_queue();
 3) ! 27273.78 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.320 us    |    }
 3) ! 27277.37 us |  }
 1)   0.501 us    |      remove_wait_queue();
 1)   0.070 us    |      _raw_spin_lock();
 1)   0.872 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 47.671 us   |      xlog_state_release_iclog [xfs]();
 1)   0.060 us    |      _raw_spin_lock();
 1)   0.231 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 3077.996 us |      }
 1)   0.261 us    |      remove_wait_queue();
 1)   0.130 us    |      _raw_spin_lock();
 1)   0.221 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6936   
 ------------------------------------------

 0) ! 3925.266 us |      }
 0)   0.231 us    |      remove_wait_queue();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.191 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.671 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.091 us    |      down_read();
 0)   0.401 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6935   
 ------------------------------------------

 2) ! 158.784 us  |      } /* xlog_cil_force_lsn [xfs] */
 2)   0.050 us    |      _raw_spin_lock();
 2)   0.381 us    |      add_wait_queue_exclusive();
 2) ! 4326.819 us |      schedule();
 2)   0.321 us    |      remove_wait_queue();
 2)   0.120 us    |      _raw_spin_lock();
 2)   0.642 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 72.529 us   |      xlog_state_release_iclog [xfs]();
 2)   0.091 us    |      _raw_spin_lock();
 2)   0.161 us    |      add_wait_queue_exclusive();
 ------------------------------------------
 2)    fio-6935    =>    fio-6934   
 ------------------------------------------

 2)               |      schedule() {
 2) ! 16321.13 us |      }
 2)   0.281 us    |      remove_wait_queue();
 2) ! 19408.81 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.611 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 15670.91 us |      } /* schedule */
 2)   0.120 us    |      remove_wait_queue();
 2) ! 19632.33 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.261 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6937   
 ------------------------------------------

 2) ! 16370.33 us |      } /* schedule */
 2)   0.111 us    |      remove_wait_queue();
 2) ! 19824.48 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.030 us    |      up_read();
 2)   0.260 us    |    }
 2) ! 19828.15 us |  }
 ------------------------------------------
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2) ! 6033.838 us |      } /* blkdev_issue_flush */
 2) ! 6037.925 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 25452.86 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0) ! 6191.178 us |      } /* blkdev_issue_flush */
 0) ! 6193.462 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 25828.78 us |  }
 ------------------------------------------
 2)    fio-6934    =>    fio-6937   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 2)   0.521 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.080 us    |      down_read();
 2)   0.320 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 17.844 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.201 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.351 us    |      filemap_check_errors();
 2)   0.571 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.060 us    |      down_read();
 2)   0.281 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.421 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.100 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.861 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.060 us    |      down_read();
 0)   0.280 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.142 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.280 us    |      add_wait_queue_exclusive();
 0) ! 9724.963 us |      schedule();
 ------------------------------------------
 2)    fio-6934    =>    fio-6935   
 ------------------------------------------

 2) ! 15546.72 us |      }
 2)   0.892 us    |      remove_wait_queue();
 2) ! 20122.97 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.100 us    |      up_read();
 2)   0.721 us    |    }
 2) ! 20129.08 us |  }
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2) ! 6679.280 us |      } /* schedule */
 2)   0.921 us    |      remove_wait_queue();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.241 us    |      xlog_state_switch_iclogs [xfs]();
 2) ! 162.860 us  |      xlog_state_release_iclog [xfs]();
 2)   0.080 us    |      _raw_spin_lock();
 2)   0.170 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2) ! 6841.821 us |      }
 2)   0.361 us    |      remove_wait_queue();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.080 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0)   0.571 us    |      remove_wait_queue();
 0)   0.511 us    |      _raw_spin_lock();
 0)   0.371 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6935   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.752 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.090 us    |      down_read();
 2)   0.330 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 28.445 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.031 us    |      _raw_spin_lock();
 2)   0.160 us    |      add_wait_queue_exclusive();
 2) ! 12573.70 us |      schedule();
 2)   0.801 us    |      remove_wait_queue();
 2)   0.441 us    |      _raw_spin_lock();
 2)   0.401 us    |      xlog_state_switch_iclogs [xfs]();
 2) ! 424.070 us  |      xlog_state_release_iclog [xfs]();
 ------------------------------------------
 3)    fio-6935    =>    fio-6934   
 ------------------------------------------

 3) ! 23335.57 us |      } /* schedule */
 3)   0.801 us    |      remove_wait_queue();
 3) ! 30187.08 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.401 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 23430.45 us |      } /* schedule */
 3)   0.181 us    |      remove_wait_queue();
 3) ! 30300.14 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.241 us    |    }
 3) ! 30304.12 us |  } /* xfs_file_fsync [xfs] */
 2)   0.160 us    |      _raw_spin_lock();
 2)   0.191 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6936   
 ------------------------------------------

 1) ! 20513.75 us |      }
 1)   0.280 us    |      remove_wait_queue();
 1) ! 30252.69 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.031 us    |      up_read();
 1)   0.251 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 64013.08 us |      blkdev_issue_flush();
 ------------------------------------------
 0)    fio-6936    =>    fio-6934   
 ------------------------------------------

 0) ! 63055.47 us |      } /* blkdev_issue_flush */
 0) ! 63057.69 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 93284.30 us |  }
 1) ! 64014.97 us |    }
 1) ! 94271.76 us |  }
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.691 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)               |      down_read() {
 3)   ==========> |
 3) ! 185.751 us  |      smp_apic_timer_interrupt();
 3)   ==========> |
 3) + 84.872 us   |      smp_apic_timer_interrupt();
 3)   0.531 us    |      } /* down_read */
 3) ! 440.898 us  |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 68.601 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.051 us    |      _raw_spin_lock();
 3)   0.171 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.380 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.331 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.491 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.090 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6934   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.541 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.080 us    |      down_read();
 1)   0.330 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.122 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.261 us    |      add_wait_queue_exclusive();
 1) ! 14969.00 us |      schedule();
 2) ! 82932.10 us |      }
 2)   0.571 us    |      remove_wait_queue();
 2) ! 95974.37 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.331 us    |    }
 2) ! 95978.42 us |  }
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 14577.78 us |      }
 3)   0.370 us    |      remove_wait_queue();
 3)   0.120 us    |      _raw_spin_lock();
 3)   0.231 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 3442.671 us |      xlog_state_release_iclog [xfs]();
 1)   0.240 us    |      remove_wait_queue();
 1)   0.090 us    |      _raw_spin_lock();
 1)   0.120 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)   0.331 us    |      _raw_spin_lock();
 3)   0.551 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.101 us    |      filemap_check_errors();
 3)   1.262 us    |    }
 3)   0.070 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.181 us    |      down_read();
 3)   0.811 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 43.923 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.070 us    |      _raw_spin_lock();
 3)   0.260 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6936   
 ------------------------------------------

 3) ! 18341.10 us |      }
 3)   0.401 us    |      remove_wait_queue();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.251 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 101190.5 us |      }
 3)   0.211 us    |      remove_wait_queue();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.320 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 1920.239 us |      xlog_state_release_iclog [xfs]();
 3)   0.090 us    |      _raw_spin_lock();
 3)   0.201 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 103463.2 us |      }
 3)   0.361 us    |      remove_wait_queue();
 3) ! 121565.7 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.360 us    |    }
 3) ! 122010.2 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 103171.2 us |      } /* schedule */
 3)   0.171 us    |      remove_wait_queue();
 3) ! 121519.6 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.270 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3) ! 9792.178 us |      blkdev_issue_flush();
 1) ! 107258.8 us |      }
 1)   0.591 us    |      remove_wait_queue();
 1) ! 122239.8 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.311 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 12101.74 us |      blkdev_issue_flush();
 3) ! 9794.543 us |    }
 3) ! 131317.8 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.491 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.091 us    |      down_read();
 3)   0.341 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 1) ! 12104.15 us |    }
 1) ! 134349.1 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.531 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.351 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 20879.62 us |      xlog_cil_force_lsn [xfs]();
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.261 us    |      filemap_check_errors();
 1)   1.132 us    |    }
 1)   0.041 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.081 us    |      down_read();
 1)   0.331 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)               |      xlog_cil_force_lsn [xfs]() {
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.501 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 26624.90 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.081 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 18593.73 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.221 us    |      _raw_spin_lock();
 3)   0.121 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 3) ! 8261.821 us |      } /* schedule */
 3)   0.591 us    |      remove_wait_queue();
 3)   0.531 us    |      _raw_spin_lock();
 3)   0.230 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 4550.877 us |      xlog_state_release_iclog [xfs]();
 1) ! 8079.209 us |      } /* schedule */
 1)   0.351 us    |      remove_wait_queue();
 2) ! 45000.07 us |      } /* schedule */
 1)   0.321 us    |      _raw_spin_lock();
 2)   0.531 us    |      remove_wait_queue();
 2) ! 148169.3 us |    } /* xfs_log_force_lsn [xfs] */
 1)   0.160 us    |      add_wait_queue_exclusive();
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 1)               |      schedule() {
 2)   0.812 us    |    }
 2) ! 148176.3 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 12639.87 us |      }
 1)   0.331 us    |      remove_wait_queue();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.221 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)   0.170 us    |      _raw_spin_lock();
 3)   0.341 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.501 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.080 us    |      down_read();
 1)   0.340 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 32.462 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.031 us    |      _raw_spin_lock();
 1)   0.120 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 2)    fio-6935    =>    fio-6934   
 ------------------------------------------

 2) ! 70399.93 us |      } /* schedule */
 2)   0.380 us    |      remove_wait_queue();
 2) ! 97084.46 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.360 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6937   
 ------------------------------------------

 2) ! 66090.35 us |      } /* schedule */
 2)   0.390 us    |      remove_wait_queue();
 2) ! 105362.6 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.331 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2) ! 11212.29 us |      blkdev_issue_flush();
 1) ! 63974.51 us |      }
 1)   0.240 us    |      remove_wait_queue();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.291 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 15.810 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.110 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1) ! 66045.00 us |      }
 1)   0.111 us    |      remove_wait_queue();
 1) ! 99752.08 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.091 us    |      up_read();
 1)   1.343 us    |    }
 1) ! 99756.70 us |  }
 2) ! 11215.05 us |    }
 2) ! 116581.7 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2) ! 11536.74 us |      } /* blkdev_issue_flush */
 2) ! 11538.41 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 108628.0 us |  } /* xfs_file_fsync [xfs] */
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.561 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.100 us    |      down_read();
 1)   0.340 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 32.903 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.041 us    |      _raw_spin_lock();
 1)   0.191 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.541 us    |    }
 3)   0.031 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.301 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   1.793 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.290 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.290 us    |    }
 3)   0.031 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.280 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.390 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.091 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 20787.91 us |      } /* schedule */
 2)   0.270 us    |      remove_wait_queue();
 2) ! 500.024 us  |      _raw_spin_lock();
 0) ! 15098.15 us |      } /* schedule */
 0)   0.641 us    |      remove_wait_queue();
 0) ! 1158.842 us |      _raw_spin_lock();
 2)   1.253 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 64.513 us   |      xlog_state_release_iclog [xfs]();
 2)   0.090 us    |      _raw_spin_lock();
 2)   0.120 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6937   
 ------------------------------------------

 2) ! 15439.36 us |      }
 2)   0.150 us    |      remove_wait_queue();
 2)   0.080 us    |      _raw_spin_lock();
 2)   0.090 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0)   0.972 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3) ! 35324.68 us |      }
 3)   0.201 us    |      remove_wait_queue();
 3) ! 99355.83 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.421 us    |    }
 3) ! 99359.18 us |  }
 ------------------------------------------
 2)    fio-6937    =>    fio-6935   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.571 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.100 us    |      down_read();
 2)   0.351 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 28.084 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.171 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6935   
 ------------------------------------------

 0) ! 6514.341 us |      }
 0)   0.280 us    |      remove_wait_queue();
 0) ! 3985.241 us |      _raw_spin_lock();
 1) ! 54080.23 us |      }
 1)   0.421 us    |      remove_wait_queue();
 1) ! 75480.71 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.160 us    |      up_read();
 1)   1.152 us    |    }
 1) ! 75502.47 us |  }
 0)   0.661 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 759.430 us  |      xlog_state_release_iclog [xfs]();
 0)   1.092 us    |      _raw_spin_lock();
 0)   0.251 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 57869.39 us |      }
 0)   0.140 us    |      remove_wait_queue();
 0) ! 74144.38 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.440 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0) ! 10714.41 us |      blkdev_issue_flush();
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 58713.15 us |      } /* schedule */
 3)   1.573 us    |      remove_wait_queue();
 3) ! 74163.24 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.331 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3) ! 10177.84 us |      blkdev_issue_flush();
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.051 us    |      filemap_check_errors();
 1)   0.882 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.501 us    |      down_read();
 1)   0.752 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 35.317 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.130 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3) ! 10181.43 us |    }
 3) ! 84349.60 us |  } /* xfs_file_fsync [xfs] */
 0) ! 10715.90 us |    }
 0) ! 84864.61 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.601 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.741 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 31.971 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.531 us    |      add_wait_queue_exclusive();
 3) ! 5646.959 us |      schedule();
 3)   0.281 us    |      remove_wait_queue();
 3)   0.111 us    |      _raw_spin_lock();
 3)   0.331 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 34.346 us   |      xlog_state_release_iclog [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.110 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.160 us    |      filemap_check_errors();
 0)   0.661 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.100 us    |      down_read();
 0)   0.652 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.683 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.410 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6935   
 ------------------------------------------

 0) ! 22017.47 us |      }
 0)   0.141 us    |      remove_wait_queue();
 0) ! 33326.64 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.291 us    |    }
 0) ! 33329.80 us |  }
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.521 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.091 us    |      down_read();
 0)   0.351 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 19.046 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.120 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 25670.73 us |      }
 3)   0.521 us    |      remove_wait_queue();
 3)   0.120 us    |      _raw_spin_lock();
 3)   0.421 us    |      add_wait_queue_exclusive();
 3) ! 2068.008 us |      schedule();
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1) ! 2068.318 us |      }
 1)   0.521 us    |      remove_wait_queue();
 1)   0.261 us    |      _raw_spin_lock();
 1)   0.702 us    |      xlog_state_switch_iclogs [xfs]();
 1) ! 172.242 us  |      xlog_state_release_iclog [xfs]();
 3)   1.143 us    |      remove_wait_queue();
 3) ! 27835.56 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.651 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 1)   0.191 us    |      _raw_spin_lock();
 1)   0.221 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2) ! 9812.009 us |      }
 2)   0.271 us    |      remove_wait_queue();
 2) ! 15535.32 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.180 us    |      up_read();
 2)   0.490 us    |    }
 2) ! 15539.58 us |  }
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 46597.20 us |      } /* schedule */
 3)   0.471 us    |      remove_wait_queue();
 3) ! 46606.13 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.320 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6936   
 ------------------------------------------

 2) ! 40971.32 us |      } /* blkdev_issue_flush */
 2) ! 40973.82 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 68816.11 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 19587.19 us |      } /* blkdev_issue_flush */
 0) ! 19591.51 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 66204.13 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.561 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.361 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 24.968 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.201 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.321 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.291 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.481 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6937   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.561 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.361 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.042 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.141 us    |      add_wait_queue_exclusive();
 0) ! 9007.140 us |      schedule();
 0)   0.651 us    |      remove_wait_queue();
 0)   0.841 us    |      _raw_spin_lock();
 0)   0.772 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 175.896 us  |      xlog_state_release_iclog [xfs]();
 0)   0.090 us    |      _raw_spin_lock();
 0)   0.180 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 1) ! 78379.16 us |      }
 1)   0.420 us    |      remove_wait_queue();
 1) ! 80653.73 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.440 us    |    }
 1) ! 80657.47 us |  }
 ------------------------------------------
 0)    fio-6937    =>    fio-6936   
 ------------------------------------------

 0) ! 12156.14 us |      }
 0)   0.421 us    |      remove_wait_queue();
 0)   0.280 us    |      _raw_spin_lock();
 0)   0.361 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6934   
 ------------------------------------------

 0) ! 12140.79 us |      }
 0)   0.130 us    |      remove_wait_queue();
 0)   0.070 us    |      _raw_spin_lock();
 0)   0.101 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6937   
 ------------------------------------------

 0) ! 20447.70 us |      }
 0)   0.240 us    |      remove_wait_queue();
 0) ! 29646.12 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.330 us    |    }
 0) ! 29649.02 us |  }
 ------------------------------------------
 0)    fio-6937    =>    fio-6936   
 ------------------------------------------

 0) ! 18340.23 us |      } /* schedule */
 0)   0.250 us    |      remove_wait_queue();
 0) ! 30531.39 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.341 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6934   
 ------------------------------------------

 0) ! 18489.69 us |      } /* schedule */
 0)   0.180 us    |      remove_wait_queue();
 0) ! 30635.49 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.351 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6937   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.501 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.351 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 16.622 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.220 us    |      xlog_state_switch_iclogs [xfs]();
 0) + 15.209 us   |      xlog_state_release_iclog [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.120 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.051 us    |      filemap_check_errors();
 1)   0.571 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.091 us    |      down_read();
 1)   0.361 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.814 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.521 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 0)    fio-6937    =>    fio-6936   
 ------------------------------------------

 0) ! 5766.668 us |      } /* blkdev_issue_flush */
 0) ! 5769.003 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 36304.86 us |  }
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2) ! 7236.183 us |      } /* blkdev_issue_flush */
 2) ! 7240.191 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 37879.28 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.692 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.091 us    |      down_read();
 2)   0.732 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) ! 2408.254 us |      xlog_cil_force_lsn [xfs]();
 2)   0.050 us    |      _raw_spin_lock();
 2)   0.241 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.300 us    |      filemap_check_errors();
 2)   1.172 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.100 us    |      down_read();
 2)   0.401 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   3.296 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.651 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 46960.76 us |      }
 3)   0.321 us    |      remove_wait_queue();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.411 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 25.499 us   |      xlog_state_release_iclog [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 4460.335 us |      }
 3)   0.130 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 72169.07 us |      }
 3)   0.491 us    |      remove_wait_queue();
 3) ! 72206.13 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.310 us    |    }
 3) ! 72209.55 us |  }
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) ! 71645.04 us |      } /* schedule */
 0)   0.471 us    |      remove_wait_queue();
 0) ! 71654.06 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.320 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.361 us    |      filemap_check_errors();
 3)   0.942 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.391 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 348.164 us  |      xlog_cil_force_lsn [xfs]();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3) ! 5445.635 us |      schedule();
 0) ! 17719.67 us |      }
 0) ! 17721.42 us |    }
 0) ! 89379.96 us |  } /* xfs_file_fsync [xfs] */
 3)   0.231 us    |      remove_wait_queue();
 3)   0.070 us    |      _raw_spin_lock();
 3)   0.311 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 75.945 us   |      xlog_state_release_iclog [xfs]();
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.051 us    |      filemap_check_errors();
 0)   0.701 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.100 us    |      down_read();
 0)   0.390 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) ! 1279.732 us |      xlog_cil_force_lsn [xfs]();
 3)   0.091 us    |      _raw_spin_lock();
 3)   0.181 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 29157.19 us |      }
 3)   0.210 us    |      remove_wait_queue();
 3) ! 78562.40 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.080 us    |      up_read();
 3)   0.441 us    |    }
 3) ! 78567.48 us |  }
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 29282.36 us |      } /* schedule */
 3)   0.271 us    |      remove_wait_queue();
 3) ! 33754.06 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.280 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.181 us    |      add_wait_queue_exclusive();
 0) ! 57684.47 us |      schedule();
 2) ! 7445.502 us |      } /* blkdev_issue_flush */
 2) ! 7448.418 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 41208.83 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.612 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.110 us    |      down_read();
 3)   0.400 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   1.413 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.371 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.511 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.090 us    |      down_read();
 2)   0.481 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 28.665 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.391 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0) + 11.482 us   |      remove_wait_queue();
 0)   1.001 us    |      _raw_spin_lock();
 0)   0.771 us    |      xlog_state_switch_iclogs [xfs]();
 0) + 75.604 us   |      xlog_state_release_iclog [xfs]();
 0)   0.111 us    |      _raw_spin_lock();
 0)   0.160 us    |      add_wait_queue_exclusive();
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0)   0.160 us    |      add_wait_queue_exclusive();
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1) ! 49995.24 us |      }
 1)   0.471 us    |      remove_wait_queue();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.141 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6937   
 ------------------------------------------

 1) ! 59601.40 us |      }
 1)   0.110 us    |      remove_wait_queue();
 1) ! 65482.08 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.260 us    |      up_read();
 1)   0.581 us    |    }
 1) ! 65487.22 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 38893.63 us |      } /* schedule */
 1)   0.210 us    |      remove_wait_queue();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.130 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.571 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.100 us    |      down_read();
 1)   0.461 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) ! 106.142 us  |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.180 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 7262.303 us |      }
 3)   0.221 us    |      remove_wait_queue();
 3)   0.181 us    |      _raw_spin_lock();
 3)   0.281 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 34.947 us   |      xlog_state_release_iclog [xfs]();
 3)   0.031 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 112308.9 us |      }
 3)   0.221 us    |      remove_wait_queue();
 3) ! 162315.8 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.351 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 112000.2 us |      } /* schedule */
 3)   0.130 us    |      remove_wait_queue();
 3) ! 150928.7 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.281 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0)   0.802 us    |      remove_wait_queue();
 0) ! 175099.9 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.351 us    |    }
 0) ! 175104.0 us |  }
 2) ! 38172.39 us |      } /* blkdev_issue_flush */
 2) ! 38175.69 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 189110.1 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6936   
 ------------------------------------------

 1) ! 43463.40 us |      } /* blkdev_issue_flush */
 1) ! 43466.29 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 205787.2 us |  }
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.100 us    |      filemap_check_errors();
 0)   0.652 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.100 us    |      down_read();
 0)   0.441 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) ! 106.954 us  |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.180 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.051 us    |      filemap_check_errors();
 0)   0.821 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.511 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 18.184 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.461 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3) ! 85112.74 us |      } /* schedule */
 3)   0.181 us    |      remove_wait_queue();
 3) ! 92526.31 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.621 us    |    }
 3) ! 92530.21 us |  }
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) ! 40392.79 us |      }
 0)   0.902 us    |      remove_wait_queue();
 0)   0.111 us    |      _raw_spin_lock();
 0)   0.370 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 2717.688 us |      xlog_state_release_iclog [xfs]();
 0)   0.291 us    |      _raw_spin_lock();
 0)   0.181 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0) ! 36930.57 us |      }
 0)   0.230 us    |      remove_wait_queue();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.100 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.070 us    |      filemap_check_errors();
 3)   0.862 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.772 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 36.600 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.180 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.181 us    |      filemap_check_errors();
 3)   0.761 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.160 us    |      down_read();
 3)   0.561 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.491 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.662 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) ! 22491.86 us |      }
 0) + 35.628 us   |      remove_wait_queue();
 ------------------------------------------
 2)    fio-6934    =>    fio-6937   
 ------------------------------------------

 2) ! 9193.910 us |      } /* schedule */
 2)   0.270 us    |      remove_wait_queue();
 2) ! 1473.804 us |      _raw_spin_lock();
 0) ! 65757.37 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.361 us    |    }
 0) ! 65760.96 us |  }
 1) ! 22673.34 us |      } /* schedule */
 1)   0.301 us    |      remove_wait_queue();
 1) ! 59631.53 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.041 us    |      up_read();
 1)   0.351 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 2)   0.651 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 17.915 us   |      xlog_state_release_iclog [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.120 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2) ! 10675.92 us |      }
 2)   0.171 us    |      remove_wait_queue();
 2) ! 10681.89 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.351 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.672 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.370 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1) ! 307.458 us  |      } /* xlog_cil_force_lsn [xfs] */
 1)   0.050 us    |      _raw_spin_lock();
 1)   0.822 us    |      add_wait_queue_exclusive();
 1) ! 32234.18 us |      schedule();
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 3582.876 us |      }
 2) ! 3585.260 us |    }
 2) ! 63222.38 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6936    =>    fio-6937   
 ------------------------------------------

 2) ! 31874.67 us |      } /* schedule */
 2)   0.290 us    |      remove_wait_queue();
 2) ! 42611.40 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.041 us    |      up_read();
 2)   0.341 us    |    }
 2) ! 42617.07 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6937    =>    fio-6936   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.051 us    |      filemap_check_errors();
 2)   0.781 us    |    }
 2)   0.031 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.090 us    |      down_read();
 2)   0.371 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 26.290 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.290 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 26.410 us   |      xlog_state_release_iclog [xfs]();
 2)   0.041 us    |      _raw_spin_lock();
 2)   0.120 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2) ! 32540.56 us |      } /* blkdev_issue_flush */
 2) ! 32541.42 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 43228.10 us |  }
 1)   0.391 us    |      remove_wait_queue();
 1)   0.170 us    |      _raw_spin_lock();
 1)   0.281 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6937   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.652 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.090 us    |      down_read();
 2)   0.421 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   2.164 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.421 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   1.373 us    |    }
 0)   0.140 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.591 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 31.931 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.180 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 84610.28 us |      }
 3)   0.240 us    |      remove_wait_queue();
 3) ! 84619.14 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.370 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 78605.14 us |      } /* schedule */
 3)   0.221 us    |      remove_wait_queue();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.662 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 15.259 us   |      xlog_state_release_iclog [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.130 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6935   
 ------------------------------------------

 3) ! 90671.90 us |      }
 3)   0.161 us    |      remove_wait_queue();
 3) ! 123226.5 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.310 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 1533.384 us |      }
 3) ! 1536.069 us |    }
 3) ! 86160.06 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 92134.05 us |      } /* schedule */
 3)   0.230 us    |      remove_wait_queue();
 3) ! 92190.88 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.281 us    |    }
 3) ! 92194.28 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 6031.821 us |      } /* blkdev_issue_flush */
 3) ! 6034.476 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 129265.1 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.161 us    |      filemap_check_errors();
 3)   0.872 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.101 us    |      down_read();
 3)   0.381 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.051 us    |      filemap_check_errors();
 3)   0.591 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.732 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   1.153 us    |    }
 3)   0.130 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.070 us    |      down_read();
 3)   0.330 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 1932.639 us |      xlog_cil_force_lsn [xfs]();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.191 us    |      add_wait_queue_exclusive();
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3)               |      schedule() {
 3) ! 4843.525 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.090 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 1976.222 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.090 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 12600.02 us |      }
 3)   0.461 us    |      remove_wait_queue();
 3)   0.391 us    |      _raw_spin_lock();
 3)   0.341 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 405.491 us  |      xlog_state_release_iclog [xfs]();
 3)   0.652 us    |      _raw_spin_lock();
 3)   0.291 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 13017.00 us |      }
 3)   0.301 us    |      remove_wait_queue();
 3)   0.071 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 27799.31 us |      }
 3)   0.120 us    |      remove_wait_queue();
 3) ! 106458.5 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.361 us    |    }
 3) ! 106464.5 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 13100.95 us |      } /* schedule */
 3)   0.170 us    |      remove_wait_queue();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.101 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.601 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 0) ! 966.775 us  |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.190 us    |      add_wait_queue_exclusive();
 0) ! 22258.76 us |      schedule();
 0)   0.251 us    |      remove_wait_queue();
 0) ! 27158.35 us |      _raw_spin_lock();
 0)   0.631 us    |      xlog_state_switch_iclogs [xfs]();
 0)               |      xlog_state_release_iclog [xfs]() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6935   
 ------------------------------------------

 3) ! 57255.92 us |      } /* schedule */
 3)   0.240 us    |      remove_wait_queue();
 3) ! 72209.98 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.361 us    |    }
 3) ! 72213.63 us |  }
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 58172.48 us |      } /* schedule */
 3)   0.251 us    |      remove_wait_queue();
 3) ! 76040.79 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.361 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 3) ! 58157.00 us |      } /* schedule */
 3)   0.281 us    |      remove_wait_queue();
 3) ! 73240.65 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.371 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.531 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.150 us    |      down_read();
 3)   0.421 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 24.286 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.041 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0) ! 2517.375 us |      }
 0)   0.110 us    |      _raw_spin_lock();
 0)   0.250 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6936   
 ------------------------------------------

 3) ! 6894.571 us |      } /* blkdev_issue_flush */
 3) ! 6897.036 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 80142.99 us |  }
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 7246.018 us |      } /* blkdev_issue_flush */
 3) ! 7248.423 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 83665.25 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.060 us    |      filemap_check_errors();
 3)   0.611 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.091 us    |      down_read();
 3)   0.441 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.150 us    |      filemap_check_errors();
 3)   0.481 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.071 us    |      down_read();
 3)   0.311 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 1126.049 us |      xlog_cil_force_lsn [xfs]();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.391 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 1167.980 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.090 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 4323.660 us |      }
 3)   0.180 us    |      remove_wait_queue();
 3)   0.070 us    |      _raw_spin_lock();
 3)   0.311 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 81.355 us   |      xlog_state_release_iclog [xfs]();
 3)   0.100 us    |      _raw_spin_lock();
 3)   0.200 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 15148.48 us |      }
 3)   0.191 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 4425.133 us |      }
 3)   0.151 us    |      remove_wait_queue();
 3)   0.070 us    |      _raw_spin_lock();
 3)   0.110 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 14678.93 us |      }
 3)   0.641 us    |      remove_wait_queue();
 3) ! 67599.91 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.371 us    |    }
 3) ! 67603.66 us |  }
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.621 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 36.079 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 23743.01 us |      }
 3)   0.201 us    |      remove_wait_queue();
 3) ! 29285.83 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.351 us    |    }
 3) ! 29288.66 us |  }
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 23908.82 us |      } /* schedule */
 3)   0.240 us    |      remove_wait_queue();
 3) ! 39087.55 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.390 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 23920.01 us |      } /* schedule */
 3)   0.121 us    |      remove_wait_queue();
 3) ! 29517.26 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.290 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6934   
 ------------------------------------------

 1) ! 7900.591 us |      }
 1)   0.782 us    |      remove_wait_queue();
 1)   0.160 us    |      _raw_spin_lock();
 1)   0.371 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 35.368 us   |      xlog_state_release_iclog [xfs]();
 1)   0.080 us    |      _raw_spin_lock();
 1)   0.271 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.591 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.360 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 341.345 us  |      xlog_cil_force_lsn [xfs]();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 8438.211 us |      } /* blkdev_issue_flush */
 3) ! 8441.046 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 47532.57 us |  }
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 68745.04 us |      } /* blkdev_issue_flush */
 1) ! 68748.48 us |    }
 1) ! 98269.96 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.060 us    |      filemap_check_errors();
 3)   0.651 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.421 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 80.043 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.511 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.661 us    |    }
 3)   0.041 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.451 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.842 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.130 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6936   
 ------------------------------------------

 3) ! 82415.07 us |      }
 3)   0.571 us    |      remove_wait_queue();
 3)   0.200 us    |      _raw_spin_lock();
 3)   0.401 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 1598.752 us |      xlog_state_release_iclog [xfs]();
 3)   0.551 us    |      _raw_spin_lock();
 3)   0.832 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 12345.80 us |      }
 3)   0.981 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3) ! 12481.44 us |      }
 3)   0.201 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6934   
 ------------------------------------------

 3) ! 84790.25 us |      }
 3)   0.130 us    |      remove_wait_queue();
 3) ! 92775.53 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.301 us    |    }
 3) ! 92779.69 us |  }
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.651 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.822 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 911.651 us  |      xlog_cil_force_lsn [xfs]();
 3)   0.070 us    |      _raw_spin_lock();
 3)   0.190 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 16533.74 us |      }
 2)   0.831 us    |      remove_wait_queue();
 2) ! 28980.12 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.360 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 9469.175 us |      } /* schedule */
 1)   0.281 us    |      remove_wait_queue();
 1)   0.321 us    |      _raw_spin_lock();
 1)   0.321 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 22.873 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.130 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6936   
 ------------------------------------------

 1) ! 16635.73 us |      }
 1)   0.141 us    |      remove_wait_queue();
 1) ! 101015.8 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.360 us    |    }
 1) ! 101020.5 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6937    =>    fio-6935   
 ------------------------------------------

 2) ! 16515.36 us |      } /* schedule */
 2)   0.250 us    |      remove_wait_queue();
 2) ! 29004.10 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.351 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2) ! 10546.68 us |      }
 2) ! 10548.98 us |    }
 2) ! 39535.21 us |  }
 ------------------------------------------
 2)    fio-6937    =>    fio-6935   
 ------------------------------------------

 2) ! 52851.24 us |      } /* blkdev_issue_flush */
 2) ! 52854.12 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 81863.28 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.100 us    |      filemap_check_errors();
 3)   0.601 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.321 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 29.236 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.180 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.041 us    |      filemap_check_errors();
 3)   0.321 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.320 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.481 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.031 us    |      filemap_check_errors();
 3)   0.311 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.340 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.351 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6934   
 ------------------------------------------

 1) ! 69385.42 us |      } /* schedule */
 1)   0.451 us    |      remove_wait_queue();
 1) ! 79801.79 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.381 us    |    }
 1) ! 79806.40 us |  } /* xfs_file_fsync [xfs] */
 1) ! 5850.989 us |      } /* schedule */
 1)   0.430 us    |      remove_wait_queue();
 1)   0.090 us    |      _raw_spin_lock();
 1)   0.260 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 28.945 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.161 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 6336.606 us |      }
 1)   0.431 us    |      remove_wait_queue();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.181 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1) ! 6320.204 us |      }
 1)   0.150 us    |      remove_wait_queue();
 1)   0.070 us    |      _raw_spin_lock();
 1)   0.101 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6934   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.571 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.100 us    |      down_read();
 1)   0.381 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 20.980 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.140 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2) ! 24288.53 us |      } /* schedule */
 2)   0.632 us    |      remove_wait_queue();
 2) ! 30208.01 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.421 us    |    }
 2) ! 30211.93 us |  } /* xfs_file_fsync [xfs] */
 1) ! 22754.17 us |      }
 1)   0.221 us    |      remove_wait_queue();
 1)   0.130 us    |      _raw_spin_lock();
 1)   0.300 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 27.272 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.160 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6935   
 ------------------------------------------

 1) ! 24138.49 us |      }
 1)   0.260 us    |      remove_wait_queue();
 1) ! 30482.82 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.371 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1) ! 24139.10 us |      } /* schedule */
 1)   0.140 us    |      remove_wait_queue();
 1) ! 30463.86 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.310 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.140 us    |      filemap_check_errors();
 2)   0.682 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.111 us    |      down_read();
 2)   0.511 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 24.728 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.180 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6935   
 ------------------------------------------

 2) ! 49902.34 us |      } /* blkdev_issue_flush */
 2) ! 49904.99 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 80391.56 us |  }
 ------------------------------------------
 2)    fio-6935    =>    fio-6936   
 ------------------------------------------

 2) ! 56605.03 us |      } /* blkdev_issue_flush */
 2) ! 56608.68 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 87075.95 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.581 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.420 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 27.312 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.431 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.030 us    |      filemap_check_errors();
 3)   0.330 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.060 us    |      down_read();
 3)   0.321 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.470 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.110 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 3) ! 4783.602 us |      } /* schedule */
 3)   0.221 us    |      remove_wait_queue();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.541 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 1052.028 us |      xlog_state_release_iclog [xfs]();
 3)   0.420 us    |      _raw_spin_lock();
 3)   0.622 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 5838.064 us |      }
 3)   0.611 us    |      remove_wait_queue();
 3)   0.160 us    |      _raw_spin_lock();
 3)   0.210 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6934   
 ------------------------------------------

 3) ! 72534.30 us |      }
 3)   0.251 us    |      remove_wait_queue();
 3) ! 95347.80 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.581 us    |    }
 3) ! 95352.28 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 68503.42 us |      } /* schedule */
 3)   0.271 us    |      remove_wait_queue();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   1.453 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.091 us    |      down_read();
 3)   0.381 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 0) ! 2312.243 us |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.251 us    |      add_wait_queue_exclusive();
 0) ! 73047.89 us |      schedule();
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 86199.38 us |      } /* schedule */
 3)   0.331 us    |      remove_wait_queue();
 3) ! 92079.89 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.371 us    |    }
 3) ! 92083.37 us |  }
 0)   0.271 us    |      remove_wait_queue();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.381 us    |      xlog_state_switch_iclogs [xfs]();
 0) + 28.826 us   |      xlog_state_release_iclog [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.120 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.111 us    |      filemap_check_errors();
 3)   1.783 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.120 us    |      down_read();
 3)   0.491 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 90302.73 us |      } /* schedule */
 3)   0.661 us    |      remove_wait_queue();
 3) ! 96151.18 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.471 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 89358.05 us |      } /* schedule */
 3)   0.230 us    |      remove_wait_queue();
 3) ! 157892.4 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.411 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3) ! 17699.63 us |      blkdev_issue_flush();
 ------------------------------------------
 0)    fio-6934    =>    fio-6936   
 ------------------------------------------

 0) ! 829.198 us  |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.130 us    |      _raw_spin_lock();
 0)   0.270 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3) ! 17702.33 us |    }
 3) ! 175600.8 us |  }
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1) ! 19801.60 us |      }
 1) ! 19804.78 us |    }
 1) ! 115959.8 us |  }
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.330 us    |      filemap_check_errors();
 1)   1.383 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.100 us    |      down_read();
 1)   0.381 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 16.181 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.501 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.561 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.110 us    |      down_read();
 1)   0.391 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.643 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.301 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 56449.73 us |      } /* schedule */
 3)   0.210 us    |      remove_wait_queue();
 3) ! 131851.4 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.361 us    |    }
 3) ! 131855.7 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 33622.98 us |      }
 1)   0.691 us    |      remove_wait_queue();
 1)   0.531 us    |      _raw_spin_lock();
 1)   0.371 us    |      xlog_state_switch_iclogs [xfs]();
 1) ! 12120.20 us |      xlog_state_release_iclog [xfs]();
 0) ! 58851.71 us |      }
 0)   0.582 us    |      remove_wait_queue();
 0)   0.110 us    |      _raw_spin_lock();
 0)   0.220 us    |      add_wait_queue_exclusive();
 0) ! 42047.78 us |      schedule();
 1)   0.241 us    |      _raw_spin_lock();
 1)   0.240 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 36802.41 us |      }
 1)   0.441 us    |      remove_wait_queue();
 1)   0.100 us    |      _raw_spin_lock();
 1)   0.260 us    |      add_wait_queue_exclusive();
 1) ! 18653.31 us |      schedule();
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.110 us    |      filemap_check_errors();
 3)   0.641 us    |    }
 3)   0.090 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.091 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 80.313 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.180 us    |      add_wait_queue_exclusive();
 3) ! 26317.68 us |      schedule();
 1)   0.481 us    |      remove_wait_queue();
 1) ! 55468.98 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.040 us    |      up_read();
 1)   0.391 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 16531.95 us |      blkdev_issue_flush();
 0)   0.631 us    |      remove_wait_queue();
 0) ! 101746.0 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.591 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 1) ! 16534.56 us |    }
 1) ! 72009.71 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 39334.32 us |      } /* schedule */
 1)   0.360 us    |      remove_wait_queue();
 1) ! 85107.24 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.371 us    |    }
 1) ! 85111.32 us |  } /* xfs_file_fsync [xfs] */
 3)   0.410 us    |      remove_wait_queue();
 3)   0.120 us    |      _raw_spin_lock();
 3)   0.310 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 27.703 us   |      xlog_state_release_iclog [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.121 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 13668.63 us |      } /* blkdev_issue_flush */
 2) ! 13671.59 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 115426.2 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.611 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.090 us    |      down_read();
 1)   0.381 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.110 us    |      filemap_check_errors();
 1)   0.360 us    |    }
 1)   0.120 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.140 us    |      down_read();
 1)   0.391 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) + 41.850 us   |      }
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.131 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) + 18.204 us   |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.071 us    |      _raw_spin_lock();
 0)   0.220 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 2)               |  xfs_file_fsync [xfs]() {/s][r=0,w=35 IOPS][eta 00m:28s]
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.561 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.090 us    |      down_read();
 2)   0.361 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   1.713 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.290 us    |      add_wait_queue_exclusive();
 2) ! 10994.84 us |      schedule();
 0) ! 69256.97 us |      }
 0)   0.871 us    |      remove_wait_queue();
 0)   1.132 us    |      _raw_spin_lock();
 0)   1.242 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 653.838 us  |      xlog_state_release_iclog [xfs]();
 0)   0.531 us    |      _raw_spin_lock();
 0)   0.341 us    |      add_wait_queue_exclusive();
 0) ! 24753.00 us |      schedule();
 1) ! 74304.63 us |      }
 1)   0.491 us    |      remove_wait_queue();
 1)   0.120 us    |      _raw_spin_lock();
 1)   0.301 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3) ! 76083.53 us |      }
 3)   0.391 us    |      remove_wait_queue();
 3) ! 102519.9 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.371 us    |    }
 3) ! 102524.9 us |  }
 2)   0.220 us    |      remove_wait_queue();
 2)   0.120 us    |      _raw_spin_lock();
 2)   0.311 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.802 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.391 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 859.721 us  |      xlog_cil_force_lsn [xfs]();
 3)   0.350 us    |      _raw_spin_lock();
 3)   0.651 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0)   0.331 us    |      remove_wait_queue();
 0) ! 94722.03 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.070 us    |      up_read();
 0)   0.732 us    |    }
 0) ! 94750.80 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 16860.52 us |      }
 1)   0.311 us    |      remove_wait_queue();
 1)   0.251 us    |      _raw_spin_lock();
 1)   0.511 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 93.028 us   |      xlog_state_release_iclog [xfs]();
 1)   0.100 us    |      _raw_spin_lock();
 1)   0.190 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 20604.90 us |      }
 1)   0.210 us    |      remove_wait_queue();
 1) ! 94961.89 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.370 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6936   
 ------------------------------------------

 1) ! 19158.40 us |      } /* schedule */
 1)   0.140 us    |      remove_wait_queue();
 1) ! 30163.32 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.301 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 2) ! 59135.71 us |      } /* blkdev_issue_flush */
 2) ! 59138.46 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 89305.29 us |  }
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2) ! 59484.71 us |      } /* schedule */
 2)   0.300 us    |      remove_wait_queue();
 2) ! 77315.54 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.371 us    |    }
 2) ! 77320.63 us |  } /* xfs_file_fsync [xfs] */
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.581 us    |    }
 0)   0.111 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.101 us    |      down_read();
 0)   0.371 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 19.808 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.031 us    |      _raw_spin_lock();
 0)   0.390 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 302.688 us  |      xlog_state_release_iclog [xfs]();
 ------------------------------------------
 1)    fio-6936    =>    fio-6937   
 ------------------------------------------

 1) ! 60263.42 us |      }
 1) ! 60264.86 us |    }
 1) ! 155230.8 us |  }
 0)   0.060 us    |      _raw_spin_lock();
 0)   0.130 us    |      add_wait_queue_exclusive();
 0) ! 20432.98 us |      schedule();
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.581 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.110 us    |      down_read();
 2)   0.421 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   1.413 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.291 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.030 us    |      filemap_check_errors();
 2)   0.320 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.070 us    |      down_read();
 2)   0.341 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.421 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.111 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.582 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.380 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 26.120 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.180 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 8667.502 us |      }
 2)   0.551 us    |      remove_wait_queue();
 2) ! 8675.958 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.351 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 2) ! 8659.436 us |      } /* schedule */
 2)   0.131 us    |      remove_wait_queue();
 2) ! 8662.041 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.040 us    |      up_read();
 2)   0.291 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6937   
 ------------------------------------------

 2) ! 5488.136 us |      } /* schedule */
 2)   0.130 us    |      remove_wait_queue();
 2)   0.190 us    |      _raw_spin_lock();
 2)   0.290 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 13.476 us   |      xlog_state_release_iclog [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.121 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 0)   0.491 us    |      remove_wait_queue();
 0) ! 20761.54 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.361 us    |    }
 0) ! 20765.12 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 14405.49 us |      } /* blkdev_issue_flush */
 3) ! 14408.48 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 23089.10 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 60447.07 us |      } /* blkdev_issue_flush */
 1) ! 60449.04 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 69114.65 us |  } /* xfs_file_fsync [xfs] */
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.672 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.090 us    |      down_read();
 1)   0.361 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 27.713 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.170 us    |      add_wait_queue_exclusive();
 1) ! 23093.80 us |      schedule();
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.110 us    |      filemap_check_errors();
 0)   0.612 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.100 us    |      down_read();
 0)   0.370 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.523 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   0.281 us    |      add_wait_queue_exclusive();
 0) ! 23255.35 us |      schedule();
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.461 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.771 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3) ! 12247.41 us |      schedule();
 3)   0.221 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.321 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 321.677 us  |      xlog_state_release_iclog [xfs]();
 3)   0.090 us    |      _raw_spin_lock();
 3)   0.201 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 95575.26 us |      }
 2)   0.541 us    |      remove_wait_queue();
 2) ! 101112.4 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.361 us    |    }
 2) ! 101116.4 us |  }
 1)   0.541 us    |      remove_wait_queue();
 1)   0.701 us    |      _raw_spin_lock();
 1) ! 23129.68 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.371 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 7343.669 us |      blkdev_issue_flush();
 0)   ==========> |
 0) + 87.497 us   |      smp_apic_timer_interrupt();
 0)   0.440 us    |      remove_wait_queue();
 0)   0.190 us    |      _raw_spin_lock();
 0) ! 23459.12 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.341 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 1) ! 7346.704 us |    }
 1) ! 30481.34 us |  }
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.050 us    |      filemap_check_errors();
 2)   0.531 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.100 us    |      down_read();
 2)   0.381 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 42.912 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.050 us    |      _raw_spin_lock();
 2)   0.230 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 32.412 us   |      xlog_state_release_iclog [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.120 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 2) ! 21276.96 us |      } /* schedule */
 2)   0.351 us    |      remove_wait_queue();
 2) ! 33856.97 us |    }
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.321 us    |    }
 2) ! 33860.74 us |  }
 ------------------------------------------
 2)    fio-6936    =>    fio-6935   
 ------------------------------------------

 2) ! 11027.13 us |      } /* blkdev_issue_flush */
 2) ! 11028.01 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 34491.54 us |  } /* xfs_file_fsync [xfs] */
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.051 us    |      filemap_check_errors();
 0)   1.242 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.441 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.030 us    |      filemap_check_errors();
 0)   0.702 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.070 us    |      down_read();
 0)   0.481 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 45.337 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.431 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) + 86.575 us   |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.101 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3) ! 3725.042 us |      }
 3)   0.271 us    |      remove_wait_queue();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.541 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 159.885 us  |      xlog_state_release_iclog [xfs]();
 3)   0.101 us    |      _raw_spin_lock();
 3)   0.181 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3) ! 3892.320 us |      }
 3)   0.180 us    |      remove_wait_queue();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.100 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 77319.61 us |      }
 3)   0.130 us    |      remove_wait_queue();
 3) ! 77399.96 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.051 us    |      up_read();
 3)   0.361 us    |    }
 3) ! 77403.76 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.521 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.361 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   1.232 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.080 us    |      filemap_check_errors();
 3)   0.771 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.360 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 43.964 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.220 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 27575.40 us |      }
 3)   0.171 us    |      remove_wait_queue();
 3) ! 31519.06 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.361 us    |    }
 3) ! 31522.59 us |  }
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 9045.677 us |      } /* schedule */
 1)   0.501 us    |      remove_wait_queue();
 1)   0.391 us    |      _raw_spin_lock();
 1)   0.581 us    |      xlog_state_switch_iclogs [xfs]();
 1) ! 479.405 us  |      xlog_state_release_iclog [xfs]();
 1)   ==========> |
 1) ! 311.384 us  |      smp_apic_timer_interrupt();
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 29314.80 us |      }
 0)   0.481 us    |      remove_wait_queue();
 0) ! 29320.62 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.351 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 1)   0.140 us    |      _raw_spin_lock();
 1)   0.180 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 30012.41 us |      }
 1)   0.241 us    |      remove_wait_queue();
 1) ! 33997.78 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.351 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1) ! 34189.54 us |      blkdev_issue_flush();
 1) ! 34192.13 us |    }
 1) ! 68196.10 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6935    =>    fio-6934   
 ------------------------------------------

 2) ! 34919.09 us |      } /* blkdev_issue_flush */
 2) ! 34921.57 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 64246.67 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.651 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 24.577 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.260 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.110 us    |      filemap_check_errors();
 1)   1.183 us    |    }
 1)   0.080 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.200 us    |      down_read();
 1)   0.812 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.523 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.090 us    |      _raw_spin_lock();
 1)   0.291 us    |      add_wait_queue_exclusive();
 1) ! 4441.258 us |      schedule();
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.110 us    |      filemap_check_errors();
 3)   0.641 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.160 us    |      down_read();
 3)   0.651 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   1.843 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.280 us    |      add_wait_queue_exclusive();
 3) ! 4236.868 us |      schedule();
 3)   0.240 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   1.914 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 819.635 us  |      xlog_state_release_iclog [xfs]();
 1)   0.501 us    |      remove_wait_queue();
 1)   0.641 us    |      _raw_spin_lock();
 1)   0.160 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 41486.47 us |      }
 1)   0.110 us    |      remove_wait_queue();
 1) ! 52702.00 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.611 us    |    }
 1) ! 52707.51 us |  }
 ------------------------------------------
 0)    fio-6934    =>    fio-6936   
 ------------------------------------------

 0) ! 4492.080 us |      } /* schedule */
 0)   0.320 us    |      remove_wait_queue();
 0)   0.110 us    |      _raw_spin_lock();
 0)   0.210 us    |      add_wait_queue_exclusive();
 0) ! 12250.95 us |      schedule();
 3)   0.100 us    |      _raw_spin_lock();
 3)   0.220 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 12199.44 us |      } /* schedule */
 1)   0.581 us    |      remove_wait_queue();
 1) ! 16657.37 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.371 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 0)   0.361 us    |      remove_wait_queue();
 0) ! 16791.33 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.351 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0) ! 10651.93 us |      blkdev_issue_flush();
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.561 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.101 us    |      down_read();
 1)   0.441 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 37.572 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.240 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 14.437 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.161 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 11789.23 us |      }
 1)   0.240 us    |      remove_wait_queue();
 1) ! 16862.68 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.351 us    |    }
 1) ! 16866.93 us |  }
 ------------------------------------------
 1)    fio-6934    =>    fio-6935   
 ------------------------------------------

 1) ! 6263.907 us |      } /* blkdev_issue_flush */
 1) ! 6267.734 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 22933.00 us |  } /* xfs_file_fsync [xfs] */
 0) ! 10654.73 us |    }
 0) ! 27450.33 us |  } /* xfs_file_fsync [xfs] */
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.050 us    |      filemap_check_errors();
 0)   0.591 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.100 us    |      down_read();
 0)   0.391 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 15774.16 us |      } /* schedule */
 1)   0.280 us    |      remove_wait_queue();
 1) ! 15830.55 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.351 us    |    }
 1) ! 15833.91 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.450 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.361 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.541 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.041 us    |      _raw_spin_lock();
 3)   0.230 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 21.862 us   |      xlog_state_release_iclog [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2) ! 396.574 us  |      } /* xlog_cil_force_lsn [xfs] */
 2)   0.050 us    |      _raw_spin_lock();
 2)   0.260 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.551 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.080 us    |      down_read();
 3)   0.511 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.731 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.030 us    |      filemap_check_errors();
 3)   0.281 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.070 us    |      down_read();
 3)   0.320 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 20.690 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.111 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 61175.13 us |      }
 2)   0.280 us    |      remove_wait_queue();
 2) ! 61578.46 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.351 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6935   
 ------------------------------------------

 2) ! 67945.25 us |      } /* schedule */
 2)   0.922 us    |      remove_wait_queue();
 2) ! 67951.94 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.060 us    |      up_read();
 2)   0.440 us    |    }
 2)               |    xfs_blkdev_issue_flush [xfs]() {
 2)               |      blkdev_issue_flush() {
 ------------------------------------------
 2)    fio-6935    =>    fio-6936   
 ------------------------------------------

 2) ! 8150.949 us |      }
 2) ! 8152.172 us |    }
 2) ! 69734.58 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2) ! 72595.03 us |      } /* schedule */
 2)   0.561 us    |      remove_wait_queue();
 2) ! 72623.85 us |    } /* xfs_log_force_lsn [xfs] */
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.341 us    |    }
 2) ! 72627.23 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6934    =>    fio-6935   
 ------------------------------------------

 2) ! 3509.649 us |      } /* blkdev_issue_flush */
 2) ! 3511.232 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 71468.50 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2) ! 71602.93 us |      } /* schedule */
 2)   0.231 us    |      remove_wait_queue();
 2)   0.100 us    |      _raw_spin_lock();
 2)   0.181 us    |      xlog_state_switch_iclogs [xfs]();
 2) ! 502.734 us  |      xlog_state_release_iclog [xfs]();
 2)   0.100 us    |      _raw_spin_lock();
 2)   0.311 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6937    =>    fio-6936   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.130 us    |      filemap_check_errors();
 2)   0.571 us    |    }
 2)   0.040 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.070 us    |      down_read();
 2)   0.341 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 17.945 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.180 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6936    =>    fio-6934   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.030 us    |      filemap_check_errors();
 2)   0.300 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.070 us    |      down_read();
 2)   0.301 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.481 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.040 us    |      _raw_spin_lock();
 2)   0.091 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6935   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 2)   0.290 us    |    }
 2)   0.110 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.061 us    |      down_read();
 2)   0.301 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   0.381 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.041 us    |      _raw_spin_lock();
 2)   0.090 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 29487.62 us |      }
 3)   0.231 us    |      remove_wait_queue();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.311 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 2669.752 us |      xlog_state_release_iclog [xfs]();
 3)   0.170 us    |      _raw_spin_lock();
 3)   0.211 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6935   
 ------------------------------------------

 3) ! 32152.35 us |      }
 3)   0.280 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.090 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 33526.81 us |      }
 3)   0.141 us    |      remove_wait_queue();
 3) ! 105662.1 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.351 us    |    }
 3) ! 105665.4 us |  }
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3) ! 32276.47 us |      } /* schedule */
 3)   0.151 us    |      remove_wait_queue();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.101 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.110 us    |      filemap_check_errors();
 3)   0.721 us    |    }
 3)   0.071 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.431 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 1652.815 us |      xlog_cil_force_lsn [xfs]();
 3)   0.060 us    |      _raw_spin_lock();
 3)   0.310 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6937   
 ------------------------------------------

 0) ! 4002.864 us |      } /* schedule */
 0)   0.551 us    |      remove_wait_queue();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.420 us    |      xlog_state_switch_iclogs [xfs]();
 0) ! 114.970 us  |      xlog_state_release_iclog [xfs]();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.130 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6937    =>    fio-6935   
 ------------------------------------------

 0) ! 44563.14 us |      }
 0)   0.691 us    |      remove_wait_queue();
 0) ! 76725.48 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.420 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 44695.07 us |      } /* schedule */
 0)   0.241 us    |      remove_wait_queue();
 0) ! 76863.63 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.401 us    |    }
 0) ! 76867.08 us |  }
 ------------------------------------------
 0)    fio-6934    =>    fio-6936   
 ------------------------------------------

 0) ! 48615.28 us |      } /* schedule */
 0)   0.501 us    |      remove_wait_queue();
 0) ! 80917.91 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.040 us    |      up_read();
 0)   0.371 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0) ! 4174.990 us |      }
 0) ! 4177.334 us |    }
 0) ! 80907.53 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 0)    fio-6935    =>    fio-6936   
 ------------------------------------------

 0) ! 5310.701 us |      } /* blkdev_issue_flush */
 0) ! 5313.547 us |    } /* xfs_blkdev_issue_flush [xfs] */
 0) ! 86236.64 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6937    =>    fio-6936   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.571 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.371 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 840.020 us  |      xlog_cil_force_lsn [xfs]();
 ------------------------------------------
 0)    fio-6936    =>    fio-6935   
 ------------------------------------------

 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.591 us    |    }
 0)   0.040 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.361 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0)               |      xlog_cil_force_lsn [xfs]() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.280 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   ==========> |
 0)               |    smp_apic_timer_interrupt() {
 0)   0.170 us    |      irq_enter();
 0)   0.051 us    |      exit_idle();
 0) + 42.581 us   |      local_apic_timer_interrupt();
 0)   2.134 us    |      irq_exit();
 0) + 84.511 us   |    }
 0)   <========== |
 0)   0.110 us    |      down_read();
 0)   0.571 us    |    } /* xfs_ilock [xfs] */
 0)               |    xfs_log_force_lsn [xfs]() {
 0)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6935   
 ------------------------------------------

 0) ! 644.170 us  |      }
 0)   0.120 us    |      _raw_spin_lock();
 0)   0.300 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 439.739 us  |      } /* xlog_cil_force_lsn [xfs] */
 0)   0.060 us    |      _raw_spin_lock();
 0)   0.181 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.130 us    |      add_wait_queue_exclusive();
 3) ! 5617.326 us |      schedule();
 ------------------------------------------
 0)    fio-6934    =>    fio-6935   
 ------------------------------------------

 0) ! 5641.008 us |      }
 0)   0.331 us    |      remove_wait_queue();
 0)   0.051 us    |      _raw_spin_lock();
 0)   0.170 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 5631.801 us |      }
 0)   0.130 us    |      remove_wait_queue();
 0)   0.071 us    |      _raw_spin_lock();
 0)   0.090 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6937   
 ------------------------------------------

 0) ! 26276.36 us |      }
 0)   0.130 us    |      remove_wait_queue();
 0) ! 32059.92 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.410 us    |    }
 0) ! 32064.92 us |  }
 3)   0.221 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.341 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 30.288 us   |      xlog_state_release_iclog [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.151 us    |      add_wait_queue_exclusive();
 3) ! 53360.95 us |      schedule();
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.631 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.090 us    |      down_read();
 1)   0.421 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 62.078 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.201 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)   0.170 us    |      remove_wait_queue();
 3) ! 59858.66 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.341 us    |    }
 3) ! 59862.48 us |  }
 ------------------------------------------
 0)    fio-6937    =>    fio-6935   
 ------------------------------------------

 0) ! 54241.83 us |      } /* schedule */
 0)   0.230 us    |      remove_wait_queue();
 0) ! 60535.91 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.340 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6935    =>    fio-6934   
 ------------------------------------------

 0) ! 56457.99 us |      } /* schedule */
 0)   0.611 us    |      remove_wait_queue();
 0) ! 62550.35 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.051 us    |      up_read();
 0)   0.411 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 1) ! 30521.31 us |      }
 1)   0.481 us    |      remove_wait_queue();
 1)   0.310 us    |      _raw_spin_lock();
 1)   0.732 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 27.693 us   |      xlog_state_release_iclog [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.121 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.561 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.451 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 55.145 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.031 us    |      _raw_spin_lock();
 3)   0.271 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 17824.70 us |      } /* blkdev_issue_flush */
 3) ! 17828.29 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 80569.04 us |  }
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   1.142 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.771 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 35.648 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   1.032 us    |      add_wait_queue_exclusive();
 3) ! 5283.145 us |      schedule();
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 24440.18 us |      } /* blkdev_issue_flush */
 1) ! 24442.73 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 84982.74 us |  }
 3)   0.160 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.321 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 102.035 us  |      xlog_state_release_iclog [xfs]();
 3)   0.091 us    |      _raw_spin_lock();
 3)   0.170 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 14039.53 us |      }
 3)   0.180 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.080 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.581 us    |    }
 3)   0.090 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.070 us    |      down_read();
 3)   0.300 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 36.680 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.040 us    |      _raw_spin_lock();
 3)   0.130 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 24562.85 us |      }
 3)   0.220 us    |      remove_wait_queue();
 3) ! 55183.01 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.321 us    |    }
 3) ! 55187.60 us |  }
 ------------------------------------------
 2)    fio-6935    =>    fio-6937   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.051 us    |      filemap_check_errors();
 2)   0.721 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.091 us    |      down_read();
 2)   0.431 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 32.933 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.041 us    |      _raw_spin_lock();
 2)   0.281 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3) ! 85589.77 us |      } /* schedule */
 3)   0.190 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.290 us    |      xlog_state_switch_iclogs [xfs]();
 3) + 79.001 us   |      xlog_state_release_iclog [xfs]();
 3)   0.080 us    |      _raw_spin_lock();
 3)   0.180 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6935    =>    fio-6934   
 ------------------------------------------

 3) ! 87002.49 us |      }
 3)   0.181 us    |      remove_wait_queue();
 3) ! 92434.25 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.371 us    |    }
 3) ! 92440.05 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 87061.01 us |      } /* schedule */
 3)   0.140 us    |      remove_wait_queue();
 3) ! 101161.5 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.281 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6937   
 ------------------------------------------

 3) ! 77342.42 us |      } /* schedule */
 3)   0.792 us    |      remove_wait_queue();
 3)   0.261 us    |      _raw_spin_lock();
 3)   0.140 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 0)    fio-6934    =>    fio-6936   
 ------------------------------------------

 0) ! 6625.804 us |      }
 0) ! 6628.288 us |    }
 0) ! 107794.6 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.541 us    |    }
 3)   0.031 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   1.683 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 9493.702 us |      xlog_cil_force_lsn [xfs]();
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.041 us    |      filemap_check_errors();
 0)   0.521 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.090 us    |      down_read();
 0)   0.351 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) ! 9841.319 us |      xlog_cil_force_lsn [xfs]();
 3) + 11.802 us   |      _raw_spin_lock();
 3)   0.210 us    |      add_wait_queue_exclusive();
 3) ! 6906.183 us |      schedule();
 0)   0.050 us    |      _raw_spin_lock();
 0)   0.160 us    |      add_wait_queue_exclusive();
 0) ! 6587.571 us |      schedule();
 1) ! 31394.14 us |      } /* schedule */
 1)   0.651 us    |      remove_wait_queue();
 1) ! 117111.6 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.341 us    |    }
 1) ! 117115.2 us |  } /* xfs_file_fsync [xfs] */
 3)   0.401 us    |      remove_wait_queue();
 3)   0.110 us    |      _raw_spin_lock();
 3)   0.430 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 399.362 us  |      xlog_state_release_iclog [xfs]();
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 30260.21 us |      } /* schedule */
 1)   0.160 us    |      remove_wait_queue();
 1) ! 107644.4 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.040 us    |      up_read();
 1)   0.271 us    |    } /* xfs_iunlock [xfs] */
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 0)   0.531 us    |      remove_wait_queue();
 0)   0.340 us    |      _raw_spin_lock();
 0)   0.170 us    |      add_wait_queue_exclusive();
 0) ! 44988.10 us |      schedule();
 3)   0.240 us    |      _raw_spin_lock();
 3)   0.360 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 2) ! 15884.28 us |      } /* blkdev_issue_flush */
 2) ! 15886.66 us |    } /* xfs_blkdev_issue_flush [xfs] */
 2) ! 123536.4 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.060 us    |      filemap_check_errors();
 3)   0.872 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.941 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 40.457 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.351 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.852 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.310 us    |      down_read();
 1)   0.591 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.182 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.151 us    |      _raw_spin_lock();
 1)   0.541 us    |      add_wait_queue_exclusive();
 1) ! 12476.60 us |      schedule();
 0)   0.291 us    |      remove_wait_queue();
 0) ! 61431.22 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.051 us    |      up_read();
 0)   0.341 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0) ! 11268.73 us |      blkdev_issue_flush();
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 53098.13 us |      }
 3)   0.531 us    |      remove_wait_queue();
 3) ! 69925.26 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.732 us    |    }
 3) ! 69931.03 us |  }
 1)   0.481 us    |      remove_wait_queue();
 1)   0.441 us    |      _raw_spin_lock();
 1)   0.310 us    |      xlog_state_switch_iclogs [xfs]();
 1) ! 452.063 us  |      xlog_state_release_iclog [xfs]();
 1)   0.130 us    |      _raw_spin_lock();
 1)   0.201 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.060 us    |      filemap_check_errors();
 3)   0.641 us    |    }
 3)   0.040 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.110 us    |      down_read();
 3)   0.440 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 156.018 us  |      xlog_cil_force_lsn [xfs]();
 0) ! 11270.72 us |    }
 0) ! 72706.33 us |  }
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.160 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 14800.27 us |      }
 3)   0.220 us    |      remove_wait_queue();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.241 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.110 us    |      filemap_check_errors();
 0)   1.052 us    |    }
 0)   0.100 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.190 us    |      down_read();
 0)   0.752 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0) + 52.190 us   |      xlog_cil_force_lsn [xfs]();
 0)   0.070 us    |      _raw_spin_lock();
 0)   0.551 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 25368.67 us |      }
 3)   0.171 us    |      remove_wait_queue();
 3)   0.061 us    |      _raw_spin_lock();
 3)   0.601 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 3155.904 us |      xlog_state_release_iclog [xfs]();
 0) ! 16115.67 us |      }
 0)   0.201 us    |      remove_wait_queue();
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.110 us    |      add_wait_queue_exclusive();
 0) ! 64217.72 us |      schedule();
 1) ! 29634.84 us |      }
 1)   0.491 us    |      remove_wait_queue();
 1) ! 42578.83 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.330 us    |    }
 1) ! 42584.39 us |  }
 3)   0.161 us    |      _raw_spin_lock();
 3)   0.711 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 28531.74 us |      }
 3)   0.210 us    |      remove_wait_queue();
 3) ! 43378.53 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.051 us    |      up_read();
 3)   0.331 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3) ! 48217.35 us |      blkdev_issue_flush();
 3) ! 48226.55 us |    }
 3) ! 91613.63 us |  }
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.050 us    |      filemap_check_errors();
 3)   0.552 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.340 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) + 29.366 us   |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.121 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0)   0.271 us    |      remove_wait_queue();
 0) ! 80395.51 us |    }
 0)               |    xfs_iunlock [xfs]() {
 0)   0.050 us    |      up_read();
 0)   0.341 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 61194.18 us |      }
 3)   0.771 us    |      remove_wait_queue();
 3) ! 89889.08 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.050 us    |      up_read();
 3)   0.431 us    |    }
 3) ! 89893.84 us |  }
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.051 us    |      filemap_check_errors();
 1)   0.501 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.091 us    |      down_read();
 1)   0.371 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.653 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.050 us    |      _raw_spin_lock();
 1)   0.251 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 18.445 us   |      xlog_state_release_iclog [xfs]();
 1)   1.513 us    |      _raw_spin_lock();
 1)   0.180 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6937   
 ------------------------------------------

 3) ! 11700.13 us |      } /* schedule */
 3)   0.131 us    |      remove_wait_queue();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.120 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1) ! 5077.940 us |      } /* blkdev_issue_flush */
 1) ! 5080.705 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 85483.15 us |  }
 ------------------------------------------KiB/s][r=0,w=46 IOPS][eta 00m:27s]
 2)    fio-6937    =>    fio-6934   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.070 us    |      filemap_check_errors();
 2)   0.811 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.070 us    |      down_read();
 2)   0.350 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 15.970 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.170 us    |      add_wait_queue_exclusive();
 2) ! 4747.887 us |      schedule();
 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.050 us    |      filemap_check_errors();
 1)   0.491 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.091 us    |      down_read();
 1)   0.361 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.721 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.031 us    |      _raw_spin_lock();
 1)   0.121 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 3) ! 38435.06 us |      }
 3)   0.201 us    |      remove_wait_queue();
 3) ! 50175.94 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.842 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3) ! 38519.25 us |      } /* schedule */
 3)   0.130 us    |      remove_wait_queue();
 3) ! 38545.00 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.181 us    |      up_read();
 3)   0.451 us    |    }
 3) ! 38548.28 us |  } /* xfs_file_fsync [xfs] */
 2)   0.410 us    |      remove_wait_queue();
 2)   0.130 us    |      _raw_spin_lock();
 2)   0.430 us    |      xlog_state_switch_iclogs [xfs]();
 2) + 21.992 us   |      xlog_state_release_iclog [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.110 us    |      add_wait_queue_exclusive();
 2) ! 27380.77 us |      schedule();
 0) ! 4922.145 us |      } /* schedule */
 0)   0.410 us    |      remove_wait_queue();
 0)   0.040 us    |      _raw_spin_lock();
 0)   0.150 us    |      add_wait_queue_exclusive();
 0) ! 25155.76 us |      schedule();
 ------------------------------------------
 3)    fio-6935    =>    fio-6937   
 ------------------------------------------

 3) ! 15470.20 us |      } /* blkdev_issue_flush */
 3) ! 15472.76 us |    } /* xfs_blkdev_issue_flush [xfs] */
 3) ! 65655.26 us |  } /* xfs_file_fsync [xfs] */
 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.041 us    |      filemap_check_errors();
 3)   0.631 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.090 us    |      down_read();
 3)   0.351 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)               |      xlog_cil_force_lsn [xfs]() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6935   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.030 us    |      filemap_check_errors();
 3)   0.271 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.150 us    |      down_read();
 3)   0.381 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3) ! 1086.581 us |      xlog_cil_force_lsn [xfs]();
 3)   0.050 us    |      _raw_spin_lock();
 3)   0.351 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 3) ! 1121.818 us |      } /* xlog_cil_force_lsn [xfs] */
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.081 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 0)   0.922 us    |      remove_wait_queue();
 0) ! 30089.20 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.090 us    |      up_read();
 0)   0.461 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1) ! 9901.334 us |      }
 1)   0.361 us    |      remove_wait_queue();
 1)   0.451 us    |      _raw_spin_lock();
 2)   0.451 us    |      remove_wait_queue();
 2) ! 32177.57 us |    }
 1)   0.300 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 26.591 us   |      xlog_state_release_iclog [xfs]();
 2)               |    xfs_iunlock [xfs]() {
 2)   0.050 us    |      up_read();
 2)   0.340 us    |    }
 2) ! 32181.90 us |  }
 1)   0.051 us    |      _raw_spin_lock();
 1)   0.110 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 9931.682 us |      }
 1)   0.130 us    |      remove_wait_queue();
 1)   0.060 us    |      _raw_spin_lock();
 1)   0.090 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6936   
 ------------------------------------------

 1) ! 8783.367 us |      } /* blkdev_issue_flush */
 1) ! 8786.503 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 38880.35 us |  }
 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.040 us    |      filemap_check_errors();
 2)   0.681 us    |    }
 2)   0.031 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.080 us    |      down_read();
 2)   0.311 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2) + 24.897 us   |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.190 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 2)    fio-6934    =>    fio-6936   
 ------------------------------------------

 2)               |  xfs_file_fsync [xfs]() {
 2)               |    filemap_write_and_wait_range() {
 2)   0.041 us    |      filemap_check_errors();
 2)   0.741 us    |    }
 2)   0.030 us    |    _raw_spin_lock();
 2)               |    xfs_ilock [xfs]() {
 2)   0.080 us    |      down_read();
 2)   0.531 us    |    }
 2)               |    xfs_log_force_lsn [xfs]() {
 2)   2.314 us    |      xlog_cil_force_lsn [xfs]();
 2)   0.030 us    |      _raw_spin_lock();
 2)   0.351 us    |      add_wait_queue_exclusive();
 2)               |      schedule() {
 ------------------------------------------
 3)    fio-6937    =>    fio-6934   
 ------------------------------------------

 3) ! 37331.80 us |      }
 3)   0.210 us    |      remove_wait_queue();
 3)   0.111 us    |      _raw_spin_lock();
 3)   0.310 us    |      xlog_state_switch_iclogs [xfs]();
 3) ! 234.688 us  |      xlog_state_release_iclog [xfs]();
 3)   0.091 us    |      _raw_spin_lock();
 3)   0.191 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 35532.60 us |      }
 3)   0.310 us    |      remove_wait_queue();
 3)   0.090 us    |      _raw_spin_lock();
 3)   0.110 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1) ! 76256.38 us |      } /* schedule */
 1)   0.541 us    |      remove_wait_queue();
 1) ! 87284.44 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.340 us    |    }
 1) ! 87287.44 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 76332.86 us |      } /* schedule */
 1)   0.130 us    |      remove_wait_queue();
 1) ! 87392.76 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.270 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3) ! 11677.61 us |      }
 3)   0.171 us    |      remove_wait_queue();
 3) ! 49281.36 us |    }
 3)               |    xfs_iunlock [xfs]() {
 3)   0.040 us    |      up_read();
 3)   0.341 us    |    }
 3) ! 49284.92 us |  }
 ------------------------------------------
 3)    fio-6934    =>    fio-6936   
 ------------------------------------------

 3) ! 11593.71 us |      } /* schedule */
 3)   0.150 us    |      remove_wait_queue();
 3) ! 47137.13 us |    } /* xfs_log_force_lsn [xfs] */
 3)               |    xfs_iunlock [xfs]() {
 3)   0.030 us    |      up_read();
 3)   0.291 us    |    }
 3)               |    xfs_blkdev_issue_flush [xfs]() {
 3)               |      blkdev_issue_flush() {
 ------------------------------------------
 0)    fio-6936    =>    fio-6937   
 ------------------------------------------

 0) ! 15335.89 us |      }
 0) ! 15338.74 us |    }
 0) ! 102735.9 us |  }
 ------------------------------------------
 1)    fio-6937    =>    fio-6936   
 ------------------------------------------

 1) ! 15053.78 us |      }
 1) ! 15057.21 us |    }
 1) ! 62199.63 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6936    =>    fio-6935   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.491 us    |    }
 1)   0.031 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.090 us    |      down_read();
 1)   0.331 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 20.138 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.300 us    |      xlog_state_switch_iclogs [xfs]();
 1) ! 1284.692 us |      xlog_state_release_iclog [xfs]();
 1)   0.080 us    |      _raw_spin_lock();
 1)   0.121 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6936   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.041 us    |      filemap_check_errors();
 1)   0.411 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.080 us    |      down_read();
 1)   0.350 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.521 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.131 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6936    =>    fio-6934   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.181 us    |      filemap_check_errors();
 1)   0.411 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.050 us    |      down_read();
 1)   0.300 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.361 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.110 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.531 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.081 us    |      down_read();
 1)   0.331 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   1.222 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.130 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 0)    fio-6937    =>    fio-6936   
 ------------------------------------------

 0) ! 52888.96 us |      } /* schedule */
 0)   0.310 us    |      remove_wait_queue();
 0) ! 52896.96 us |    } /* xfs_log_force_lsn [xfs] */
 0)               |    xfs_iunlock [xfs]() {
 0)   0.271 us    |      up_read();
 0)   0.681 us    |    }
 0)               |    xfs_blkdev_issue_flush [xfs]() {
 0) ! 13476.18 us |      blkdev_issue_flush();
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 52998.72 us |      }
 1)   0.451 us    |      remove_wait_queue();
 1) ! 54310.44 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.320 us    |    }
 1) ! 54314.64 us |  }
 ------------------------------------------
 1)    fio-6935    =>    fio-6934   
 ------------------------------------------

 1) ! 52976.20 us |      } /* schedule */
 1)   0.391 us    |      remove_wait_queue();
 1) ! 52978.93 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.261 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 49939.93 us |      } /* schedule */
 1)   0.100 us    |      remove_wait_queue();
 1) ! 49944.87 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.030 us    |      up_read();
 1)   0.260 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6934   
 ------------------------------------------

 1) ! 12618.05 us |      }
 1) ! 12620.75 us |    }
 1) ! 65602.99 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6934    =>    fio-6937   
 ------------------------------------------

 1) ! 13208.60 us |      } /* blkdev_issue_flush */
 1) ! 13209.58 us |    } /* xfs_blkdev_issue_flush [xfs] */
 1) ! 63157.92 us |  } /* xfs_file_fsync [xfs] */
 0) ! 13478.72 us |    }
 0) ! 66381.16 us |  } /* xfs_file_fsync [xfs] */
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.040 us    |      filemap_check_errors();
 1)   0.781 us    |    }
 1)   0.040 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.080 us    |      down_read();
 1)   0.461 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1) + 31.801 us   |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.200 us    |      xlog_state_switch_iclogs [xfs]();
 1) + 27.101 us   |      xlog_state_release_iclog [xfs]();
 1)   0.040 us    |      _raw_spin_lock();
 1)   0.110 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1)               |  xfs_file_fsync [xfs]() {
 1)               |    filemap_write_and_wait_range() {
 1)   0.030 us    |      filemap_check_errors();
 1)   0.310 us    |    }
 1)   0.030 us    |    _raw_spin_lock();
 1)               |    xfs_ilock [xfs]() {
 1)   0.060 us    |      down_read();
 1)   0.591 us    |    }
 1)               |    xfs_log_force_lsn [xfs]() {
 1)   0.350 us    |      xlog_cil_force_lsn [xfs]();
 1)   0.030 us    |      _raw_spin_lock();
 1)   0.101 us    |      add_wait_queue_exclusive();
 1)               |      schedule() {
 0)               |  xfs_file_fsync [xfs]() {
 0)               |    filemap_write_and_wait_range() {
 0)   0.040 us    |      filemap_check_errors();
 0)   0.681 us    |    }
 0)   0.030 us    |    _raw_spin_lock();
 0)               |    xfs_ilock [xfs]() {
 0)   0.081 us    |      down_read();
 0)   0.431 us    |    }
 0)               |    xfs_log_force_lsn [xfs]() {
 0)   1.573 us    |      xlog_cil_force_lsn [xfs]();
 0)   0.030 us    |      _raw_spin_lock();
 0)   ==========> |
 0) + 75.515 us   |      smp_apic_timer_interrupt();
 0)   0.461 us    |      add_wait_queue_exclusive();
 0)               |      schedule() {
 ------------------------------------------
 3)    fio-6936    =>    fio-6934   
 ------------------------------------------

 3)               |  xfs_file_fsync [xfs]() {
 3)               |    filemap_write_and_wait_range() {
 3)   0.040 us    |      filemap_check_errors();
 3)   0.441 us    |    }
 3)   0.030 us    |    _raw_spin_lock();
 3)               |    xfs_ilock [xfs]() {
 3)   0.100 us    |      down_read();
 3)   0.441 us    |    }
 3)               |    xfs_log_force_lsn [xfs]() {
 3)   0.461 us    |      xlog_cil_force_lsn [xfs]();
 3)   0.030 us    |      _raw_spin_lock();
 3)   0.131 us    |      add_wait_queue_exclusive();
 3)               |      schedule() {
 ------------------------------------------
 1)    fio-6937    =>    fio-6935   
 ------------------------------------------

 1) ! 14576.41 us |      }
 1)   0.561 us    |      remove_wait_queue();
 1) ! 14640.77 us |    }
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.321 us    |    }
 1) ! 14644.67 us |  }
 ------------------------------------------
 1)    fio-6935    =>    fio-6937   
 ------------------------------------------

 1) ! 14724.71 us |      } /* schedule */
 1)   0.702 us    |      remove_wait_queue();
 1) ! 14729.43 us |    } /* xfs_log_force_lsn [xfs] */
 1)               |    xfs_iunlock [xfs]() {
 1)   0.050 us    |      up_read();
 1)   0.321 us    |    }
 1)               |    xfs_blkdev_issue_flush [xfs]() {
 1)               |      blkdev_issue_flush() {
^C
fio: terminating on signal 2

Ending tracing...

myjob: (groupid=0, jobs=1): err= 0: pid=6934: Wed Dec 27 19:12:56 2023
  write: IOPS=11, BW=45.8KiB/s (46.9kB/s)(144KiB/3143msec)
    clat (usec): min=1860, max=77952, avg=15998.80, stdev=18530.31
     lat (usec): min=1862, max=77953, avg=15999.89, stdev=18530.31
    clat percentiles (usec):
     |  1.00th=[ 1860],  5.00th=[ 1991], 10.00th=[ 2245], 20.00th=[ 2999],
     | 30.00th=[ 5604], 40.00th=[ 7373], 50.00th=[11207], 60.00th=[12780],
     | 70.00th=[15401], 80.00th=[17171], 90.00th=[34341], 95.00th=[70779],
     | 99.00th=[78119], 99.50th=[78119], 99.90th=[78119], 99.95th=[78119],
     | 99.99th=[78119]
   bw (  KiB/s): min=   30, max=   63, per=24.23%, avg=44.33, stdev=13.32, samples=6
   iops        : min=    7, max=   15, avg=10.50, stdev= 3.33, samples=6
  lat (msec)   : 2=5.56%, 4=16.67%, 10=22.22%, 20=36.11%, 50=11.11%
  lat (msec)   : 100=8.33%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=16, max=189, avg=71.08, stdev=36.95
    sync percentiles (msec):
     |  1.00th=[   17],  5.00th=[   17], 10.00th=[   25], 20.00th=[   39],
     | 30.00th=[   47], 40.00th=[   66], 50.00th=[   69], 60.00th=[   78],
     | 70.00th=[   90], 80.00th=[   93], 90.00th=[  109], 95.00th=[  136],
     | 99.00th=[  190], 99.50th=[  190], 99.90th=[  190], 99.95th=[  190],
     | 99.99th=[  190]
  cpu          : usr=0.00%, sys=6.84%, ctx=141, majf=0, minf=34
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,36,0,36 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=6935: Wed Dec 27 19:12:56 2023
  write: IOPS=11, BW=46.4KiB/s (47.5kB/s)(144KiB/3102msec)
    clat (usec): min=1079, max=74353, avg=19525.54, stdev=22493.03
     lat (usec): min=1080, max=74354, avg=19526.57, stdev=22493.07
    clat percentiles (usec):
     |  1.00th=[ 1074],  5.00th=[ 1106], 10.00th=[ 2057], 20.00th=[ 3752],
     | 30.00th=[ 4359], 40.00th=[ 6521], 50.00th=[ 8029], 60.00th=[13566],
     | 70.00th=[16450], 80.00th=[42206], 90.00th=[61604], 95.00th=[68682],
     | 99.00th=[73925], 99.50th=[73925], 99.90th=[73925], 99.95th=[73925],
     | 99.99th=[73925]
   bw (  KiB/s): min=   30, max=   63, per=23.50%, avg=43.00, stdev=12.41, samples=6
   iops        : min=    7, max=   15, avg=10.17, stdev= 3.13, samples=6
  lat (msec)   : 2=8.33%, 4=13.89%, 10=27.78%, 20=22.22%, 50=13.89%
  lat (msec)   : 100=13.89%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=13, max=175, avg=68.32, stdev=40.07
    sync percentiles (msec):
     |  1.00th=[   14],  5.00th=[   15], 10.00th=[   21], 20.00th=[   23],
     | 30.00th=[   39], 40.00th=[   55], 50.00th=[   72], 60.00th=[   81],
     | 70.00th=[   86], 80.00th=[   95], 90.00th=[  117], 95.00th=[  148],
     | 99.00th=[  176], 99.50th=[  176], 99.90th=[  176], 99.95th=[  176],
     | 99.99th=[  176]
  cpu          : usr=0.00%, sys=4.71%, ctx=138, majf=0, minf=33
  IO depths    : 1=197.2%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,36,0,35 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=6936: Wed Dec 27 19:12:56 2023
  write: IOPS=11, BW=45.8KiB/s (46.9kB/s)(144KiB/3141msec)
    clat (usec): min=1595, max=69116, avg=17399.35, stdev=19162.82
     lat (usec): min=1597, max=69117, avg=17400.43, stdev=19162.79
    clat percentiles (usec):
     |  1.00th=[ 1598],  5.00th=[ 1631], 10.00th=[ 2769], 20.00th=[ 4817],
     | 30.00th=[ 5342], 40.00th=[ 8160], 50.00th=[ 9372], 60.00th=[12125],
     | 70.00th=[15795], 80.00th=[27657], 90.00th=[61080], 95.00th=[64750],
     | 99.00th=[68682], 99.50th=[68682], 99.90th=[68682], 99.95th=[68682],
     | 99.99th=[68682]
   bw (  KiB/s): min=   30, max=   63, per=24.23%, avg=44.33, stdev=13.32, samples=6
   iops        : min=    7, max=   15, avg=10.50, stdev= 3.33, samples=6
  lat (msec)   : 2=5.56%, 4=8.33%, 10=38.89%, 20=22.22%, 50=13.89%
  lat (msec)   : 100=11.11%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=18, max=205, avg=69.77, stdev=37.98
    sync percentiles (msec):
     |  1.00th=[   20],  5.00th=[   22], 10.00th=[   24], 20.00th=[   34],
     | 30.00th=[   40], 40.00th=[   63], 50.00th=[   69], 60.00th=[   79],
     | 70.00th=[   88], 80.00th=[   92], 90.00th=[  108], 95.00th=[  132],
     | 99.00th=[  207], 99.50th=[  207], 99.90th=[  207], 99.95th=[  207],
     | 99.99th=[  207]
  cpu          : usr=0.10%, sys=3.47%, ctx=148, majf=0, minf=32
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,36,0,36 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=6937: Wed Dec 27 19:12:56 2023
  write: IOPS=11, BW=46.3KiB/s (47.4kB/s)(144KiB/3111msec)
    clat (usec): min=995, max=104781, avg=19250.11, stdev=23231.33
     lat (usec): min=996, max=104782, avg=19251.10, stdev=23231.52
    clat percentiles (usec):
     |  1.00th=[   996],  5.00th=[  1020], 10.00th=[  1287], 20.00th=[  2278],
     | 30.00th=[  6259], 40.00th=[  9503], 50.00th=[ 10159], 60.00th=[ 13566],
     | 70.00th=[ 21103], 80.00th=[ 25560], 90.00th=[ 54264], 95.00th=[ 68682],
     | 99.00th=[104334], 99.50th=[104334], 99.90th=[104334], 99.95th=[104334],
     | 99.99th=[104334]
   bw (  KiB/s): min=   30, max=   63, per=24.23%, avg=44.33, stdev=11.24, samples=6
   iops        : min=    7, max=   15, avg=10.50, stdev= 2.81, samples=6
  lat (usec)   : 1000=2.78%
  lat (msec)   : 2=11.11%, 4=8.33%, 10=22.22%, 20=25.00%, 50=16.67%
  lat (msec)   : 100=11.11%, 250=2.78%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=10, max=175, avg=66.93, stdev=42.11
    sync percentiles (msec):
     |  1.00th=[   11],  5.00th=[   15], 10.00th=[   16], 20.00th=[   30],
     | 30.00th=[   31], 40.00th=[   53], 50.00th=[   66], 60.00th=[   78],
     | 70.00th=[   92], 80.00th=[  102], 90.00th=[  123], 95.00th=[  155],
     | 99.00th=[  176], 99.50th=[  176], 99.90th=[  176], 99.95th=[  176],
     | 99.99th=[  176]
  cpu          : usr=0.06%, sys=3.57%, ctx=145, majf=0, minf=32
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,36,0,36 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=183KiB/s (188kB/s), 45.8KiB/s-46.4KiB/s (46.9kB/s-47.5kB/s), io=576KiB (590kB), run=3102-3143msec

Disk stats (read/write):
    dm-2: ios=0/352, merge=0/0, ticks=0/5366, in_queue=5367, util=82.60%, aggrios=331/368, aggrmerge=9/341, aggrticks=6550/5754, aggrin_queue=12302, aggrutil=95.33%
  sda: ios=331/368, merge=9/341, ticks=6550/5754, in_queue=12302, util=95.33%
^C
Message from syslogd@localhost at Dec 27 19:13:44 ...
 kernel: NMI watchdog: BUG: soft lockup - CPU#1 stuck for 22s! [funcgraph:6910]
[pratikj@localhost NewBcc]$ gedit 27script.sh
[pratikj@localhost NewBcc]$ gedit 27script.sh
[pratikj@localhost NewBcc]$ gedit 27job.fio
[pratikj@localhost NewBcc]$ gedit 27script.sh
[pratikj@localhost NewBcc]$ chmod +x 27count.sh
[pratikj@localhost NewBcc]$ sudo ./27count.sh
[sudo] password for pratikj: 
Tracing 1 functions for "filemap_write_and_wait_range"... Hit Ctrl-C to end.
myjob: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=sync, iodepth=1
...
fio-3.7
Starting 4 processes
Jobs: 4 (f=4): [w(4)][100.0%][r=0KiB/s,w=484KiB/s][r=0,w=121 IOPS][eta 00m:00s]
myjob: (groupid=0, jobs=1): err= 0: pid=7356: Wed Dec 27 19:34:54 2023
  write: IOPS=34, BW=138KiB/s (142kB/s)(4152KiB/30017msec)
    clat (usec): min=1079, max=56999, avg=6266.55, stdev=4546.48
     lat (usec): min=1080, max=57001, avg=6268.32, stdev=4546.87
    clat percentiles (usec):
     |  1.00th=[ 1418],  5.00th=[ 1844], 10.00th=[ 2073], 20.00th=[ 2638],
     | 30.00th=[ 3294], 40.00th=[ 4146], 50.00th=[ 5538], 60.00th=[ 6325],
     | 70.00th=[ 8160], 80.00th=[ 9503], 90.00th=[11207], 95.00th=[12518],
     | 99.00th=[19530], 99.50th=[30540], 99.90th=[42206], 99.95th=[56886],
     | 99.99th=[56886]
   bw (  KiB/s): min=   80, max=  176, per=24.91%, avg=137.73, stdev=23.35, samples=60
   iops        : min=   20, max=   44, avg=34.00, stdev= 5.85, samples=60
  lat (msec)   : 2=8.29%, 4=30.25%, 10=44.89%, 20=15.70%, 50=0.77%
  lat (msec)   : 100=0.10%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=8, max=153, avg=22.61, stdev= 9.27
    sync percentiles (msec):
     |  1.00th=[   12],  5.00th=[   13], 10.00th=[   15], 20.00th=[   17],
     | 30.00th=[   20], 40.00th=[   21], 50.00th=[   22], 60.00th=[   23],
     | 70.00th=[   25], 80.00th=[   27], 90.00th=[   30], 95.00th=[   36],
     | 99.00th=[   57], 99.50th=[   71], 99.90th=[  109], 99.95th=[  155],
     | 99.99th=[  155]
  cpu          : usr=0.52%, sys=10.32%, ctx=4249, majf=0, minf=33
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1038,0,1038 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7357: Wed Dec 27 19:34:54 2023
  write: IOPS=34, BW=138KiB/s (142kB/s)(4156KiB/30011msec)
    clat (usec): min=958, max=85792, avg=6321.01, stdev=4460.28
     lat (usec): min=960, max=85794, avg=6322.21, stdev=4460.40
    clat percentiles (usec):
     |  1.00th=[ 1090],  5.00th=[ 1844], 10.00th=[ 2704], 20.00th=[ 4359],
     | 30.00th=[ 4883], 40.00th=[ 5276], 50.00th=[ 5669], 60.00th=[ 5997],
     | 70.00th=[ 6390], 80.00th=[ 7439], 90.00th=[10290], 95.00th=[12125],
     | 99.00th=[20579], 99.50th=[28181], 99.90th=[44827], 99.95th=[85459],
     | 99.99th=[85459]
   bw (  KiB/s): min=   79, max=  176, per=24.93%, avg=137.88, stdev=23.57, samples=60
   iops        : min=   19, max=   44, avg=34.13, stdev= 5.90, samples=60
  lat (usec)   : 1000=0.48%
  lat (msec)   : 2=5.68%, 4=10.01%, 10=72.67%, 20=10.01%, 50=1.06%
  lat (msec)   : 100=0.10%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=11, max=240, avg=22.54, stdev=10.01
    sync percentiles (msec):
     |  1.00th=[   14],  5.00th=[   16], 10.00th=[   17], 20.00th=[   18],
     | 30.00th=[   19], 40.00th=[   20], 50.00th=[   21], 60.00th=[   23],
     | 70.00th=[   24], 80.00th=[   26], 90.00th=[   30], 95.00th=[   34],
     | 99.00th=[   59], 99.50th=[   66], 99.90th=[   82], 99.95th=[  241],
     | 99.99th=[  241]
  cpu          : usr=0.45%, sys=8.99%, ctx=4153, majf=0, minf=32
  IO depths    : 1=199.9%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1039,0,1038 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7358: Wed Dec 27 19:34:54 2023
  write: IOPS=34, BW=138KiB/s (142kB/s)(4148KiB/30005msec)
    clat (usec): min=993, max=32377, avg=6269.58, stdev=4310.34
     lat (usec): min=994, max=32378, avg=6270.80, stdev=4310.40
    clat percentiles (usec):
     |  1.00th=[ 1450],  5.00th=[ 1860], 10.00th=[ 2114], 20.00th=[ 2606],
     | 30.00th=[ 3130], 40.00th=[ 3687], 50.00th=[ 4490], 60.00th=[ 6521],
     | 70.00th=[ 8586], 80.00th=[10028], 90.00th=[11469], 95.00th=[13566],
     | 99.00th=[21103], 99.50th=[22676], 99.90th=[29230], 99.95th=[32375],
     | 99.99th=[32375]
   bw (  KiB/s): min=   79, max=  176, per=24.88%, avg=137.57, stdev=23.65, samples=60
   iops        : min=   19, max=   44, avg=33.90, stdev= 5.97, samples=60
  lat (usec)   : 1000=0.10%
  lat (msec)   : 2=6.94%, 4=37.51%, 10=35.20%, 20=19.00%, 50=1.25%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=10, max=153, avg=22.64, stdev= 9.72
    sync percentiles (msec):
     |  1.00th=[   12],  5.00th=[   13], 10.00th=[   15], 20.00th=[   17],
     | 30.00th=[   19], 40.00th=[   20], 50.00th=[   22], 60.00th=[   23],
     | 70.00th=[   25], 80.00th=[   27], 90.00th=[   31], 95.00th=[   36],
     | 99.00th=[   63], 99.50th=[   73], 99.90th=[  102], 99.95th=[  155],
     | 99.99th=[  155]
  cpu          : usr=0.43%, sys=10.84%, ctx=4263, majf=0, minf=31
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1037,0,1037 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7359: Wed Dec 27 19:34:54 2023
  write: IOPS=34, BW=139KiB/s (142kB/s)(4156KiB/30007msec)
    clat (usec): min=1194, max=56612, avg=6371.75, stdev=4655.12
     lat (usec): min=1195, max=56614, avg=6373.47, stdev=4655.01
    clat percentiles (usec):
     |  1.00th=[ 1483],  5.00th=[ 1876], 10.00th=[ 2212], 20.00th=[ 2704],
     | 30.00th=[ 3163], 40.00th=[ 3949], 50.00th=[ 4948], 60.00th=[ 6521],
     | 70.00th=[ 8586], 80.00th=[ 9896], 90.00th=[11338], 95.00th=[12911],
     | 99.00th=[21890], 99.50th=[28181], 99.90th=[43254], 99.95th=[56361],
     | 99.99th=[56361]
   bw (  KiB/s): min=   79, max=  176, per=24.94%, avg=137.92, stdev=23.53, samples=60
   iops        : min=   19, max=   44, avg=34.08, stdev= 5.92, samples=60
  lat (msec)   : 2=6.74%, 4=34.36%, 10=39.36%, 20=18.38%, 50=1.06%
  lat (msec)   : 100=0.10%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=8, max=146, avg=22.46, stdev= 9.18
    sync percentiles (msec):
     |  1.00th=[   12],  5.00th=[   13], 10.00th=[   15], 20.00th=[   17],
     | 30.00th=[   19], 40.00th=[   21], 50.00th=[   22], 60.00th=[   23],
     | 70.00th=[   24], 80.00th=[   26], 90.00th=[   31], 95.00th=[   36],
     | 99.00th=[   60], 99.50th=[   70], 99.90th=[  109], 99.95th=[  146],
     | 99.99th=[  146]
  cpu          : usr=0.54%, sys=10.81%, ctx=4275, majf=0, minf=32
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1039,0,1039 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=553KiB/s (567kB/s), 138KiB/s-139KiB/s (142kB/s-142kB/s), io=16.2MiB (17.0MB), run=30005-30017msec

Disk stats (read/write):
    dm-2: ios=0/10364, merge=0/0, ticks=0/60414, in_queue=60427, util=91.69%, aggrios=0/10417, aggrmerge=0/8, aggrticks=0/61933, aggrin_queue=61912, aggrutil=92.35%
  sda: ios=0/10417, merge=0/8, ticks=0/61933, in_queue=61912, util=92.35%
^C
FUNC                                    COUNT
filemap_write_and_wait_range             4152
Detaching...
[pratikj@localhost NewBcc]$ gedit 27count.sh
[pratikj@localhost NewBcc]$ sudo ./27count.sh
myjob: (g=0): rw=randwrite, bs=(R) 4096B-4096B, (W) 4096B-4096B, (T) 4096B-4096B, ioengine=sync, iodepth=1
...
fio-3.7
Starting 4 processes
Tracing 1 functions for "filemap_write_and_wait_range"... Hit Ctrl-C to end.
Jobs: 4 (f=4): [w(4)][100.0%][r=0KiB/s,w=644KiB/s][r=0,w=161 IOPS][eta 00m:00s]
myjob: (groupid=0, jobs=1): err= 0: pid=7421: Wed Dec 27 19:37:31 2023
  write: IOPS=40, BW=161KiB/s (165kB/s)(4832KiB/30013msec)
    clat (usec): min=937, max=73258, avg=5166.13, stdev=3132.09
     lat (usec): min=939, max=73260, avg=5167.21, stdev=3132.11
    clat percentiles (usec):
     |  1.00th=[ 1004],  5.00th=[ 1434], 10.00th=[ 1926], 20.00th=[ 3130],
     | 30.00th=[ 4359], 40.00th=[ 4686], 50.00th=[ 4948], 60.00th=[ 5276],
     | 70.00th=[ 5735], 80.00th=[ 6390], 90.00th=[ 8455], 95.00th=[ 9372],
     | 99.00th=[13173], 99.50th=[15926], 99.90th=[20055], 99.95th=[72877],
     | 99.99th=[72877]
   bw (  KiB/s): min=   71, max=  183, per=24.97%, avg=160.55, stdev=17.51, samples=60
   iops        : min=   17, max=   45, avg=39.77, stdev= 4.49, samples=60
  lat (usec)   : 1000=0.91%
  lat (msec)   : 2=9.60%, 4=13.99%, 10=72.27%, 20=3.15%, 100=0.08%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=8, max=191, avg=19.60, stdev= 6.54
    sync percentiles (msec):
     |  1.00th=[   12],  5.00th=[   15], 10.00th=[   16], 20.00th=[   17],
     | 30.00th=[   18], 40.00th=[   18], 50.00th=[   19], 60.00th=[   20],
     | 70.00th=[   21], 80.00th=[   22], 90.00th=[   25], 95.00th=[   27],
     | 99.00th=[   33], 99.50th=[   39], 99.90th=[   62], 99.95th=[  192],
     | 99.99th=[  192]
  cpu          : usr=0.54%, sys=9.57%, ctx=4816, majf=0, minf=33
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1208,0,1208 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7422: Wed Dec 27 19:37:31 2023
  write: IOPS=40, BW=161KiB/s (165kB/s)(4828KiB/30015msec)
    clat (usec): min=1047, max=70384, avg=5284.98, stdev=3879.91
     lat (usec): min=1048, max=70385, avg=5287.60, stdev=3881.08
    clat percentiles (usec):
     |  1.00th=[ 1287],  5.00th=[ 1680], 10.00th=[ 1893], 20.00th=[ 2180],
     | 30.00th=[ 2540], 40.00th=[ 2933], 50.00th=[ 3752], 60.00th=[ 5473],
     | 70.00th=[ 7832], 80.00th=[ 8717], 90.00th=[ 9765], 95.00th=[10814],
     | 99.00th=[14484], 99.50th=[17433], 99.90th=[20841], 99.95th=[70779],
     | 99.99th=[70779]
   bw (  KiB/s): min=   71, max=  183, per=24.92%, avg=160.23, stdev=17.44, samples=60
   iops        : min=   17, max=   45, avg=39.62, stdev= 4.43, samples=60
  lat (msec)   : 2=13.67%, 4=37.37%, 10=40.51%, 20=8.29%, 50=0.08%
  lat (msec)   : 100=0.08%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=8, max=195, avg=19.51, stdev= 7.31
    sync percentiles (msec):
     |  1.00th=[   11],  5.00th=[   13], 10.00th=[   14], 20.00th=[   16],
     | 30.00th=[   17], 40.00th=[   19], 50.00th=[   20], 60.00th=[   21],
     | 70.00th=[   22], 80.00th=[   23], 90.00th=[   25], 95.00th=[   28],
     | 99.00th=[   34], 99.50th=[   42], 99.90th=[   88], 99.95th=[  197],
     | 99.99th=[  197]
  cpu          : usr=0.85%, sys=9.96%, ctx=4982, majf=0, minf=32
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1207,0,1207 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7423: Wed Dec 27 19:37:31 2023
  write: IOPS=40, BW=161KiB/s (165kB/s)(4824KiB/30009msec)
    clat (usec): min=1011, max=69576, avg=5691.31, stdev=3946.36
     lat (usec): min=1012, max=69577, avg=5693.15, stdev=3945.89
    clat percentiles (usec):
     |  1.00th=[ 1369],  5.00th=[ 1696], 10.00th=[ 1942], 20.00th=[ 2245],
     | 30.00th=[ 2638], 40.00th=[ 3195], 50.00th=[ 4752], 60.00th=[ 6521],
     | 70.00th=[ 8455], 80.00th=[ 9241], 90.00th=[10159], 95.00th=[11076],
     | 99.00th=[14091], 99.50th=[15533], 99.90th=[20317], 99.95th=[69731],
     | 99.99th=[69731]
   bw (  KiB/s): min=   63, max=  183, per=24.95%, avg=160.43, stdev=18.04, samples=60
   iops        : min=   15, max=   45, avg=39.83, stdev= 4.63, samples=60
  lat (msec)   : 2=12.44%, 4=33.83%, 10=42.54%, 20=11.03%, 50=0.08%
  lat (msec)   : 100=0.08%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=7, max=195, avg=19.12, stdev= 7.37
    sync percentiles (msec):
     |  1.00th=[   11],  5.00th=[   12], 10.00th=[   13], 20.00th=[   15],
     | 30.00th=[   17], 40.00th=[   18], 50.00th=[   20], 60.00th=[   21],
     | 70.00th=[   22], 80.00th=[   23], 90.00th=[   25], 95.00th=[   27],
     | 99.00th=[   36], 99.50th=[   40], 99.90th=[   82], 99.95th=[  197],
     | 99.99th=[  197]
  cpu          : usr=0.66%, sys=9.83%, ctx=4933, majf=0, minf=31
  IO depths    : 1=200.0%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1206,0,1206 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1
myjob: (groupid=0, jobs=1): err= 0: pid=7424: Wed Dec 27 19:37:31 2023
  write: IOPS=40, BW=161KiB/s (165kB/s)(4828KiB/30002msec)
    clat (usec): min=942, max=69543, avg=5199.15, stdev=3713.95
     lat (usec): min=942, max=69544, avg=5200.93, stdev=3714.12
    clat percentiles (usec):
     |  1.00th=[ 1106],  5.00th=[ 1516], 10.00th=[ 1860], 20.00th=[ 2278],
     | 30.00th=[ 2638], 40.00th=[ 3163], 50.00th=[ 4490], 60.00th=[ 5211],
     | 70.00th=[ 6587], 80.00th=[ 8586], 90.00th=[ 9634], 95.00th=[10683],
     | 99.00th=[14091], 99.50th=[15533], 99.90th=[21365], 99.95th=[69731],
     | 99.99th=[69731]
   bw (  KiB/s): min=   64, max=  184, per=24.94%, avg=160.35, stdev=17.69, samples=60
   iops        : min=   16, max=   46, avg=39.78, stdev= 4.43, samples=60
  lat (usec)   : 1000=0.25%
  lat (msec)   : 2=13.42%, 4=32.23%, 10=46.64%, 20=7.21%, 50=0.17%
  lat (msec)   : 100=0.08%
  fsync/fdatasync/sync_file_range:
    sync (msec): min=7, max=187, avg=19.60, stdev= 7.05
    sync percentiles (msec):
     |  1.00th=[   12],  5.00th=[   13], 10.00th=[   14], 20.00th=[   16],
     | 30.00th=[   18], 40.00th=[   19], 50.00th=[   20], 60.00th=[   21],
     | 70.00th=[   22], 80.00th=[   23], 90.00th=[   25], 95.00th=[   28],
     | 99.00th=[   35], 99.50th=[   40], 99.90th=[   78], 99.95th=[  188],
     | 99.99th=[  188]
  cpu          : usr=0.82%, sys=9.46%, ctx=4905, majf=0, minf=32
  IO depths    : 1=199.9%, 2=0.0%, 4=0.0%, 8=0.0%, 16=0.0%, 32=0.0%, >=64=0.0%
     submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
     issued rwts: total=0,1207,0,1206 short=0,0,0,0 dropped=0,0,0,0
     latency   : target=0, window=0, percentile=100.00%, depth=1

Run status group 0 (all jobs):
  WRITE: bw=643KiB/s (659kB/s), 161KiB/s-161KiB/s (165kB/s-165kB/s), io=18.9MiB (19.8MB), run=30002-30015msec

Disk stats (read/write):
    dm-2: ios=0/12016, merge=0/0, ticks=0/60184, in_queue=60194, util=91.29%, aggrios=252/12092, aggrmerge=0/440, aggrticks=27381/62737, aggrin_queue=89704, aggrutil=92.83%
  sda: ios=252/12092, merge=0/440, ticks=27381/62737, in_queue=89704, util=92.83%
^C
     nsecs               : count     distribution
         0 -> 1          : 0        |                                        |
         2 -> 3          : 0        |                                        |
         4 -> 7          : 0        |                                        |
         8 -> 15         : 0        |                                        |
        16 -> 31         : 0        |                                        |
        32 -> 63         : 0        |                                        |
        64 -> 127        : 0        |                                        |
       128 -> 255        : 0        |                                        |
       256 -> 511        : 0        |                                        |
       512 -> 1023       : 264      |***                                     |
      1024 -> 2047       : 778      |***********                             |
      2048 -> 4095       : 2812     |****************************************|
      4096 -> 8191       : 581      |********                                |
      8192 -> 16383      : 1        |                                        |
     16384 -> 32767      : 21       |                                        |
     32768 -> 65535      : 6        |                                        |
     65536 -> 131071     : 8        |                                        |
    131072 -> 262143     : 25       |                                        |
    262144 -> 524287     : 7        |                                        |
    524288 -> 1048575    : 0        |                                        |
   1048576 -> 2097151    : 1        |                                        |
   2097152 -> 4194303    : 1        |                                        |
   4194304 -> 8388607    : 2        |                                        |
Detaching...