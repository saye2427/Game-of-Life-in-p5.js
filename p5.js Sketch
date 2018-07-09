var grid;
var speed = 1;
var mouseClicks = 0;

function setup () {
  createCanvas(400, 400);
  frameRate(speed);
  
  grid = new Grid(10);
  grid.randomize();
  
  reset();
}

function draw () {
  background(250);
  
  grid.updateNeighborCounts();
  grid.updatePopulation();

  grid.draw();
}

class Grid {
  constructor (cellSize) {
    this.cellSize = cellSize;

    this.numberOfColumns = width / cellSize;
    this.numberOfRows = height / cellSize;

    var x = this.numberOfColumns;
    var y = this.numberOfRows;
    this.cells = new Array(x);
    for (var i = 0; i < this.cells.length; i++) {
      this.cells[i] = new Array(y);
    }

    for (var column = 0; column < this.numberOfColumns; column++) {
      for (var row = 0; row < this.numberOfRows; row++) {
        this.cells[column][row] = new Cell(column, row, cellSize);
      }
    }
    print(this.cells);
  }

  draw () {
    for (var column = 0; column < this.numberOfColumns; column ++) {
      for (var row = 0; row < this.numberOfRows; row++) {
        this.cells[column][row].draw();
      }
    }
  }
  
  randomize() {
    for (var column = 0; column < this.numberOfColumns; column ++) {
      for (var row = 0; row < this.numberOfRows; row++) {
        this.cells[column][row].setIsAlive(floor(random(2)));
      }
    }
  }
  
  updatePopulation() {
    for (var column = 0; column < this.numberOfColumns; column ++) {
      for (var row = 0; row < this.numberOfRows; row ++) {
        this.cells[column][row].liveOrDie();
      }
    }
  }
  
  getNeighbors(currentCell) {
    var neighbors = [];
    
    //add logic to get neighbors and add them to the Array
    for (var xOffset = -1; xOffset <= 1; xOffset ++) {
      for (var yOffset = -1; yOffset <= 1; yOffset ++) {
        var neighborColumn = currentCell.column + xOffset;
        var neighborRow = currentCell.row + yOffset;
        
        if (this.isValidPosition(neighborColumn, neighborRow) === true && neighborColumn === currentCell.column && neighborRow === currentCell.row) {
          //do something with neighborColumn and neighborRow
            neighbors = neighbors;
        } else if (this.isValidPosition(neighborColumn, neighborRow) === true) {
          neighbors.push(this.cells[neighborColumn][neighborRow]);
        }
      }
    }
    return neighbors;
  }
  
  isValidPosition(column, row) {
    if (column >= 0 && column < this.numberOfColumns && row >= 0 && row < this.numberOfRows) {
      return true;
    } else {
      return false;
    }
  }
  
  updateNeighborCounts() {
    for (var column = 0; column < this.numberOfColumns; column ++) {
      for (var row = 0; row < this.numberOfRows; row ++) {
        this.cells[column][row].liveNeighborCount = 0;

        var cellNeighbors = [];
        cellNeighbors = grid.getNeighbors(this.cells[column][row]);

        for (var i = 0; i < cellNeighbors.length; i ++) {
          if (cellNeighbors[i].isAlive === true) {
            this.cells[column][row].liveNeighborCount ++;
          }
        }
      }
    }
  }
}

class Cell {
  constructor(column, row, size) {
    this.column = column;
    this.row = row;
    this.size = size;

    this.isAlive = false;
    this.liveNeighborCount = 0;
  }
  
  draw() {
    if (this.isAlive === false) {
      fill(50);
    } else {
      fill(255, 150, 0);
    }
    noStroke();
    rect(this.column * this.size + 1, this.row * this.size + 1, this.size - 1, this.size - 1);
  }
  
  setIsAlive(value) {
    if (value === 1) {
      this.isAlive = true;
    } else {
      this.isAlive = false;
    }
  }
  
  liveOrDie() {
    if (this.isAlive === true) {
      if (this.liveNeighborCount < 2 || this.liveNeighborCount > 3) {
        this.isAlive = false;
      } else if (this.liveNeighborCount === 2 || this.liveNeighborCount === 3) {
        this.isAlive = true;
      }
    } else {
      if (this.liveNeighborCount === 3) {
        this.isAlive = true;
      }
    }
  }
}

function mousePressed() {
  mouseClicks ++;
  if (mouseClicks %2 === 1) {
    frameRate(0);
  } else if (mouseClicks %2 === 0) {
    frameRate(1);
  }
}

function keyPressed() {
  if (keyCode === ENTER) {
    frameRate(speed ++);
  } else if (keyCode === SHIFT) {
    reset();
  }
}

function reset() {
  createCanvas(400, 400);
  frameRate(1);
  
  grid = new Grid(10);
  grid.randomize();
}
