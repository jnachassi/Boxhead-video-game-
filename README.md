# Boxhead-video-game-
shooting fun game 


_root.attachMovie("hero","hero",_root.getNextHighestDepth(),{_x:250, _y:200});
_root.attachMovie("zombie","zombie",_root.getNextHighestDepth(),{_x:25, _y:20});
hero_speed = 1.5;
zombie_speed = 1;
zombie.same_rotation = 0;
hero.onEnterFrame = function() {
	xspeed = 0;
	yspeed = 0;
	if (Key.isDown(Key.LEFT)) {
		xspeed -= hero_speed;
	}
	if (Key.isDown(Key.RIGHT)) {
		xspeed += hero_speed;
	}
	if (Key.isDown(Key.UP)) {
		yspeed -= hero_speed;
	}
	if (Key.isDown(Key.DOWN)) {
		yspeed += hero_speed;
	}
	if ((xspeed != 0) and (yspeed != 0)) {
		xspeed *= 0.707;
		yspeed *= 0.707;
	}
	this._x += xspeed;
	this._y += yspeed;
	switch (xspeed) {
		case hero_speed :
			this._rotation = 90;
			break;
		case -hero_speed :
			this._rotation = -90;
			break;
		default :
			switch (yspeed) {
				case hero_speed :
					this._rotation = 180;
					break;
				case -hero_speed :
					this._rotation = 0;
					break;
				case hero_speed*0.707 :
					if (xspeed == hero_speed*0.707) {
						this._rotation = 135;
					}
					if (xspeed -= hero_speed*0.707) {
						this._rotation = -135;
					}
					break;
				case -hero_speed*0.707 :
					if (xspeed == hero_speed*0.707) {
						this._rotation = 45;
					}
					if (xspeed -= hero_speed*0.707) {
						this._rotation = -45;
					}
					break;
			}
	}
};
zombie.onEnterFrame = function() {
	this.same_rotation++;
	dist_x = this._x-hero._x;
	dist_y = this._y-hero._y;
	angle = Math.atan2(dist_y, dist_x);
	real_rotation = angle*57.2957795-90;
	this._save_rotation = this._rotation;
	if (this.same_rotation>15) {
		this._rotation = Math.round(real_rotation/45)*45;
	}
	if (this._rotation != this._save_rotation) {
		this.same_rotation = 0;
	}
	switch (this._rotation) {
		case 0 :
			this._y -= zombie_speed;
			break;
		case 45 :
			this._y -= zombie_speed*0.707;
			this._x += zombie_speed*0.707;
			break;
		case 90 :
			this._x += zombie_speed;
			break;
		case 135 :
			this._y += zombie_speed*0.707;
			this._x += zombie_speed*0.707;
			break;
		case -180 :
			this._y += zombie_speed;
			break;
		case -135 :
			this._y += zombie_speed*0.707;
			this._x -= zombie_speed*0.707;
			break;
		case -90 :
			this._x -= zombie_speed;
			break;
		case -45 :
			this._y -= zombie_speed*0.707;
			this._x -= zombie_speed*0.707;
			break;
	}
};
