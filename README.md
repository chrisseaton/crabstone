crabstone
====

Current library support: 4.0.1
----

( FROM THE CAPSTONE README )

Capstone is a disassembly framework with the target of becoming the ultimate
disasm engine for binary analysis and reversing in the security community.

Created by Nguyen Anh Quynh, then developed and maintained by a small community,
Capstone offers some unparalleled features:

- Support multiple hardware architectures: ARM, ARM64 (aka ARMv8), Mips, X86, Sparc & SystemZ.

- Having clean/simple/lightweight/intuitive architecture-neutral API.

- Provide details on disassembled instruction (called “decomposer” by others).

- Provide semantics of the disassembled instruction, such as list of implicit
     registers read & written.

- Implemented in pure C language, with lightweight wrappers for C++, Python,
     Ruby, OCaml, C#, Java and Go available.

- Native support for Windows & *nix platforms (MacOSX, Linux & *BSD confirmed).

- Thread-safe by design.

- Distributed under the open source BSD license.

To install:
----

First install the capstone library from either https://github.com/aquynh/capstone
or http://www.capstone-engine.org

Then:

```bash
gem install crabstone
```

To write code:
----

Check the tests in [Capstone](https://github.com/aquynh/capstone) for more examples. Here is "Hello World":
```ruby

require 'crabstone'
include Crabstone
arm =
  "\xED\xFF\xFF\xEB\x04\xe0\x2d\xe5\x00\x00\x00\x00\xe0\x83\x22" \
  "\xe5\xf1\x02\x03\x0e\x00\x00\xa0\xe3\x02\x30\xc1\xe7\x00\x00\x53\xe3"

begin
  cs = Disassembler.new(ARCH_ARM, MODE_ARM)
  puts "Hello from Capstone v#{cs.version.join('.')}!"
  puts 'Disasm:'

  begin
    cs.disasm(arm, 0x1000).each do |i|
      printf("0x%x:\t%s\t\t%s\n", i.address, i.mnemonic, i.op_str)
    end
  rescue StandardError => e
    raise "Disassembly error: #{e.message}"
  ensure
    cs.close
  end
rescue StandardError => e
  raise "Unable to open engine: #{e.message}"
end
```

Contributing:
----

If you feel like chipping in, especially with better tests or examples, or (please!!) documentation, fork and send me a pull req.


	Library Author: Nguyen Anh Quynh
	Binding Authors: Nguyen Anh Quynh, Tan Sheng Di, Ben Nagy
	License: BSD style - details in the LICENSE file
	(c) 2013 COSEINC. All Rights Reserved.

