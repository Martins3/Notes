# Port dune to mips
- [ ] 如何交叉编译从而可以让我在 x86 的电脑上看内核 ?


# We will finishes it 10 days

## question before write
- hypercall 
  - [ ] cause BD : something instruction emulation

- [x] syscall
  - We have to recompile glibc
  - [x] enter the guest mode in the usermode, maybe we have to adjust some register value to indicate the usermode.
    - x86 : 如果没有配置 MSR_LSTAR 的话，而是使用 int 80, 那么会执行 idt 中间的地址
    - [x] mips : syscall 的手册 : 
  - [x] MIPS virtualization manual :  4.7.4 Exception Priority
    - [x] A guest enabled interrupt occurred. / A root enabled interrupt occurred. : how to confict ? junru wang's paper says it's dangerous

- tdp
  - [x] pte_mkclean / pte_mkold
    - pte_mkold : used by notifier
    - pte_mkclean : used by map page fast 
  - [ ] mmu notifier
    - [x] invalidate_range_start
    - [x] invalidate_range_end
    - [x] clear_flush_young  
    - [x] clear_young
    - [x] test_young
    - [x] change_pte : **I think dune will never call this function**
    - [x] release
  - [ ] invalid TLB
  - [ ] asid

-  kvm_mips_handle_exit
  - kvm_trap_vz_handle_tlb_ld_miss + kvm_trap_vz_handle_tlb_st_miss
    - *kvm_mips_handle_vz_root_tlb_fault*
      - kvm_mips_map_page
        - [ ] kvm_mips_set_pmd_huge
      - kvm_vz_host_tlb_inv

- relation between kvm_mips_flush_gpa_pt && kvm_vz_host_tlb_inv && kvm_mips_flush_gva_pt
  - kvm_mips_flush_gva_pt : used by emulate.c at which we're not interested
  - kvm_mips_flush_gpa_pt : mmu notifier, used for invalid page table translation from `gpa -> gpa`
  - kvm_vz_host_tlb_inv : load miss / store miss exception

- entry
  - [x] why need assembly code to return to host ? because we have something more to restore, such as host register
    - [x] RESUME_HOST to userspace.
  - [ ] **TLB exception handler is managed by software, so we have to setup the TLB entry before enter to guest software.**
    - Now that we have already setup entry for the guset software, of course, change the syscall entry is possible too.
      - [x] is supporting kernel mode syscall and user mode syscall possible ?
        - YES, x86 remap the page,  MIPS rewrite the code

- [ ] user mode architectural code ?

- memslot : substituted by our wired **dune_vm_map_pages**

## clean and old
how mips handle clean and old page in the host ?


## user mode

- [ ] entry.c
  - [ ] setup_safe_stack
  - [ ] fs / gs register
  - [ ] percpu
  - [ ] enter guset
- [x] vm.c