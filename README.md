# rack.scad.
# Python script to generate OpenSCAD file for a 4-level adjustable sanding disc rack

scad_code = """ 
// Adjustable Sanding Disc Rack
// Generated via Python Script

// Parameters
disc_diameter = 254; // 10 inches in mm
disc_thickness = 5; // Approximate thickness of each sanding disc
min_spacing = 76; // 3 inches in mm
max_spacing = 152; // 6 inches in mm
support_width = 30; // Width of side supports
rack_depth = disc_thickness * 3 + 10; // Extra depth for stability
num_levels = 4; // Number of levels

// Base Platform
module base() {
    cube([disc_diameter + 2 * support_width, rack_depth, 10]);
}

// Side Supports with Adjustable Slots
module side_support() {
    for (i = [0:num_levels-1]) {
        y_offset = (i + 1) * min_spacing + 10;
        translate([0, y_offset, 0])
            cube([support_width, rack_depth, 5]); // Side supports with spacing
    }
}

// Adjustable Shelves
module shelves() {
    for (i = [0:num_levels-1]) {
        z_offset = (i + 1) * min_spacing + 10;
        translate([support_width, 0, z_offset])
            cube([disc_diameter, rack_depth, disc_thickness]); // Create shelves
    }
}

// Assemble Rack
module rack() {
    base();
    side_support();
    shelves();
}

// Render the rack
rack();
"""

# Write the OpenSCAD script to a file
with open("rack.scad", "w") as file:
    file.write(scad_code)

print("Generated 'rack.scad'. Open it in OpenSCAD to view and export as STL.")
