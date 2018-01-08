# Open Hardware Construction Platform

Open Hardware Construction Platform is a multi-lingual software framework for describing digital systems using popular software programming languages.

    // Pseudocode
    
    build_adder(module m) {
        node a = m.add_port("a", IN, array(logic, WIDTH));      // Add a port to the module
        node b = m.add_port("b", IN, array(logic, WIDTH));
        node c;
        if (add_3) {                                            // Conditionally add a port
            c = m.add_port("b", IN, array(logic, WIDTH));
        }
        node o = m.add_port("o", OUT, array(logic, WIDTH));
        
        if (add_3) {
            o = a + b + c;
        } else {
            o = a + b;
        }
    }
    
    module_descr adder = {
        .build = build_adder
    }
    
    main() {
        module a0 = module_create(adder, "a0");
        
        synthesize(a0);
        dump_sysverilog(a0, "file.sv");
    }

## Acknowledgments

_I humbly present this work to The Supreme Protector who resides in the beautiful temple at the heart of Guruvayur town_

_Special thanks to my parents, my uncle and my cousin for their support in my scientific endeavors_

## About

*Work in progress*
