# Open Hardware Construction Platform

Open Hardware Construction Platform is a multi-lingual software framework for describing digital systems using popular software programming languages.

    // Pseudocode
    
    build_adder(module m) {
        node a = m.add_port(array(logic, WIDTH), IN, "a");      // Add a port to the module
        node b = m.add_port(array(logic, WIDTH), IN, "b");
        node c;
        if (add_3) {                                            // Conditionally add a port
            c = m.add_port(array(logic, WIDTH), IN, "b");
        }
        node o = m.add_port(array(logic, WIDTH), OUT, "o");
        
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
        
        module_destroy(a0);
    }

## About

*Work in progress*

## Quick Reference

* Modules: Similar to verilog modules, consists of ports, internal nodes and child module instances
* Node: A junction/net that can hold a value. Nodes are designated a specific data type and are driven by expressions
* Expression: Blob that takes one or more nodes as inputs and generates a single output
* Port: A node on the interface of a module. Can be input or output. Contains an internal node with a specific data type.
* Type: A runtime data structure that describes the "type" of a node. Can be of three types:
    - Atomic: bit/logic
    - Array: Classic array. Multi-dimensional are created using array of arrays
    - Aggregate: Similar to struct. Effectively a name-type mapping
* Handle: A unique ID to a heap-allocated object that holds an object of module/node etc. Depending on the language in force, might be an int, pointer or reference.

All objects of module, node, expression, port and types are heap allocated.

### Node

    node_handle_t n0 = node_create(type_handle_t t, string name)    // Create
    node_destroy(n0)                                                // Destroy
    
### Port

    port_handle_t p0 = port_create(type_handle_t t, port_dir dir, string name)  // Create
    port_destroy(p0)                                                            // Destroy

### Module

    // Build module in a function
    build_func(module_handle_t m) {
        a = m.create_port(type, IN, "a")        // Add port to this module. Returns handle to created port
        b = m.create_port(type, IN, "b")
        c = m.create_port(type, OUT, "c")
        
        d = m.create_node(type, "d")            // Internal node
        
        d = a + b                               // Expression. Links nodes. Links internal nodes when ports
        c = d + 1;                              // are involved
                                                // Syntax depends on language. In C, we'd need to use
                                                // node_assign(c, expr_add_int(d, 1))
    }
    
    // Plug build_func into a module descriptor structure
    module_descr descr = {
        .build  = build_func
    }
    
    // Create module instances
    module_handle_t m = module_create(descr, name)
    
    // Use the module instance
    dump_to_verilog(m)
    
... Work in progress ...

