# chromedino 
Hack game chromedino offline hoặc chromedino.com

# Code tăng speed
var over=Runner.prototype.gameOver;
Runner.instance_.setSpeed(1000); //thay 1000 thành số lớn hơn nếu muốn điểm tăng nhanh hơn!

# hoặc code này cũng tăng speed
var over=Runner.prototype.gameOver;
Runner.prototype.gameOver = function ()
{
	Runner.instance_.setSpeed(Runner.instance_.currentSpeed+2)
};

# Code bất tử
var over=Runner.prototype.gameOver;
Runner.prototype.gameOver = ()=>{};

# Code phóng to thu nhỏ con khủng long
scale = 2; // Sửa tỉ lệ tại đây
Runner.instance_.tRex.config.HEIGHT_REAL = Runner.instance_.tRex.config.HEIGHT;
Runner.instance_.tRex.config.WIDTH_REAL = Runner.instance_.tRex.config.WIDTH;
Runner.instance_.tRex.config.WIDTH_DUCK_REAL =
Runner.instance_.tRex.config.WIDTH_DUCK;
Runner.instance_.tRex.config.HEIGHT *= scale;
Runner.instance_.tRex.config.WIDTH *= scale;
Runner.instance_.tRex.config.HEIGHT_DUCK *= scale;
Runner.instance_.tRex.config.WIDTH_DUCK *= scale;
Runner.instance_.tRex.yPos -=
Runner.instance_.tRex.config.HEIGHT -
Runner.instance_.tRex.config.HEIGHT_REAL;
Runner.instance_.tRex.groundYPos -=
Runner.instance_.tRex.config.HEIGHT -
Runner.instance_.tRex.config.HEIGHT_REAL;
Runner.instance_.tRex.__proto__.draw = function(x, y) {
  var sourceX = x;
  var sourceY = y;
  var sourceWidth =
    this.ducking && this.status != "CRASHED"
      ? this.config.WIDTH_DUCK_REAL
      : this.config.WIDTH_REAL;
  var sourceHeight = this.config.HEIGHT_REAL;

  if (window.devicePixelRatio > 1) {
    sourceX *= 2;
    sourceY *= 2;
    sourceWidth *= 2;
    sourceHeight *= 2;
  }

  // Adjustments for sprite sheet position.
  sourceX += this.spritePos.x;
  sourceY += this.spritePos.y;

  // Ducking.
  if (this.ducking && this.status != "CRASHED") {
    this.canvasCtx.drawImage(
      Runner.imageSprite,
      sourceX,
      sourceY,
      sourceWidth,
      sourceHeight,
      this.xPos,
      this.yPos,
      this.config.WIDTH_DUCK,
      this.config.HEIGHT
    );
  } else {
    // Crashed whilst ducking. Trex is standing up so needs adjustment.
    if (this.ducking && this.status == "CRASHED") {
      this.xPos++;
    }
    // Standing / running
    this.canvasCtx.drawImage(
      Runner.imageSprite,
      sourceX,
      sourceY,
      sourceWidth,
      sourceHeight,
      this.xPos,
      this.yPos,
      this.config.WIDTH,
      this.config.HEIGHT
    );
  }
};

# Stop game nhưng vẫn lưu điểm được
var over=Runner.prototype.gameOver;
Runner.prototype.gameOver=over;
