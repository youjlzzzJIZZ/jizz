安装依赖 首先，确保你已经安装了Flask和SQLAlchemy：

bash pip install Flask SQLAlchemy 数据库模型 python from flask import Flask from flask_sqlalchemy import SQLAlchemy

app = Flask(name) app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///jobs.db' app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False db = SQLAlchemy(app)

class User(db.Model): id = db.Column(db.Integer, primary_key=True) username = db.Column(db.String(80), unique=True, nullable=False) password = db.Column(db.String(120), nullable=False) role = db.Column(db.String(20), nullable=False) # 'employer' or 'jobseeker'

class Job(db.Model): id = db.Column(db.Integer, primary_key=True) title = db.Column(db.String(100), nullable=False) company = db.Column(db.String(100), nullable=False) skills = db.Column(db.Text, nullable=False) posted_by = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)

class Resume(db.Model): id = db.Column(db.Integer, primary_key=True) user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False) education = db.Column(db.Text, nullable=False) experience = db.Column(db.Text, nullable=False) skills = db.Column(db.Text, nullable=False)
