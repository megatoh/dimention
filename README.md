// Function to create dimension lines between two objects
function createDimension() {
    var doc = app.activeDocument;
    var selection = doc.selection;
    
    if (selection.length != 2) {
        alert("Select two objects to create dimensions between.");
        return;
    }
    
    var obj1 = selection[0];
    var obj2 = selection[1];
    
    var group = doc.groupItems.add();
    
    var line1 = group.pathItems.add();
    line1.setEntirePath([[obj1.left, obj1.top], [obj2.left, obj1.top]]);
    
    var line2 = group.pathItems.add();
    line2.setEntirePath([[obj2.left, obj1.top], [obj2.left, obj2.top]]);
    
    var text = group.textFrames.add();
    var distance = Math.abs(obj2.left - obj1.left);
    text.contents = distance.toFixed(2) + " pt"; // Display distance in points
    
    text.position = [obj1.left + distance / 2, obj1.top - 12]; // Adjust the position of the text
}

// Call the createDimension function
createDimension();

