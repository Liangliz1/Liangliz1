---
layout: post
title: "Rsearch"
categories: Dwelling
author:
- Asher
meta: "Springfield"
---

Early Research:



#include<iostream>
using namespace std;
#include<string>
#define MAX 1000

struct Person
{
	string m_Name;
	int m_Sex;
	int m_Age;
	string m_Phone;
	string m_Addr;
};

struct Addressbooks
{
	struct Person personArray[MAX];
	int m_Size;
};

//1.添加联系人
void addPerson(Addressbooks* abs)
{
	if (abs->m_Size == MAX)
	{
		cout << "通讯录已满，无法添加" << endl;
		return;
	}
	else
	{
		//添加具体的联系人
		string name;
		cout << "请输入姓名:  " << endl;
		cin >> name;
		abs->personArray[abs->m_Size].m_Name = name;  //将此姓名放入通讯录数组,如果用结构体变量访问，'点.'属性即可，指针利用箭头访问结构体中的数据。
				                                      //通过结构体指针访问结构体中的属性，需要利用‘->’
		//性别
		cout << "请输入性别:  " << endl;
		cout << "1.代表男生" << endl;
		cout << "2.代表女生" << endl;
		int sex = 0;
		while (true)   //假死循环，防止用户输入除1，2其他的数
		{
			cin >> sex;  //在这一步，用户输入姓名
			if (sex == 1 || sex == 2)  //输入1或者2，可以退出循环，如果输入其他，循环重新输入
			{
				abs->personArray[abs->m_Size].m_Sex = sex;  

				break;   //如果用户输入正确，则退出这个循环
			}
			cout << "输入有误，请重新输入！" << endl;
		}

		//年龄
		cout << "请输入年龄:  " << endl;
		int age = 0;
		while (true)
		{
			cin >> age;
			if (age >= 0 && age <= 100)
			{
				abs->personArray[abs->m_Size].m_Age = age;
				break;
			}
			cout << "您的输入是错的" << endl;
		}
		
		//电话
		cout << "请输入电话" << endl;
		string phone;
		cin >> phone;
		abs->personArray[abs->m_Size].m_Phone = phone;

		//住址
		cout << "最后请输入住址：  " << endl;
		string addr;
		cin >> addr;
		abs->personArray[abs->m_Size].m_Addr = addr;

		//更新通讯录人数
		abs->m_Size++;  //通讯录人数加1

		//完成添加提示
		cout << "恭喜您添加成功！" << endl;

		system("pause");  //按任意键继续
		system("cls");    //清屏操作
	}
}    

//2.显示联系人
void showPerson(Addressbooks* abs)
{
	if (abs->m_Size == 0)
	{
		cout << "当前记录为空" << endl;
	}
	else
	{
		for (int i = 0; i < abs->m_Size; i++)
		{
			cout << "姓名：" << abs->personArray[i].m_Name << "\t";
			cout << "性别：" << (abs->personArray[i].m_Sex == 1 ? "男" : "女") << "\t";
			cout << "年龄：" << abs->personArray[i].m_Age << "\t";
			cout << "电话：" << abs->personArray[i].m_Phone << "\t";
			cout << "住址：" << abs->personArray[i].m_Addr << endl;
		}
	}

	system("pause");
	system("cls");

}

//3.检测联系人是否存在
int isExist(Addressbooks* abs, string name)
{
	for (int i = 0; i < abs->m_Size; i++)
	{
		//找到用户
		if (abs->personArray[i].m_Name == name)
			return i;
	}
	return -1;
}


//4.删除联系人
void deletePerson(Addressbooks* abs)
{
	cout << "请输入您要删除的联系人:  " << endl;

	string name;
	cin >> name;

	int ret = isExist(abs, name);

	if (ret != -1)
	{
		for (int i = ret; i < abs->m_Size; i++)
		{
			abs->personArray[i] = abs->personArray[i + 1];
		}
		abs->m_Size--;
		cout << "删除成功" << endl;
	}
	else
	{
		cout << "查无此人" << endl;
	}
}

//5.查找联系人
void findPerson(Addressbooks* abs)
{
	cout << "请输入您要查找的联系人" << endl;
	string name;
	cin >> name;

	int ret = isExist(abs, name);

	if (ret != -1)
	{
		cout << "姓名:  " << abs->personArray[ret].m_Name << "\t";
		cout << "性别:  " << (abs->personArray[ret].m_Sex == 1 ? "男" : "女") << "\t";
		cout << "年龄:  " << abs->personArray[ret].m_Age << "\t";
		cout << "电话:  " << abs->personArray[ret].m_Phone << "\t";
		cout << "地址:  " << abs->personArray[ret].m_Addr<< "\t";
	}
	else
	{
		cout << "查无此人" << endl;
	}
	system("pause");
	system("cls");
}

//6.修改联系人
void modifyPerson(Addressbooks* abs)
{
	cout << "请输入您要修改的联系人" << endl;
	string name;
	cin >> name;

	int ret = isExist(abs, name);
	if (ret != -1)
	{
		//姓名
		string name;
		cout << "请输入姓名：" << endl;
		cin >> name;
		abs->personArray[ret].m_Name = name;

		cout << "请输入性别：" << endl;
		cout << "1 -- 男" << endl;
		cout << "2 -- 女" << endl;

		//性别
		int sex = 0;
		while (true)
		{
			cin >> sex;
			if (sex == 1 || sex == 2)
			{
				abs->personArray[ret].m_Sex = sex;
				break;
			}
			cout << "输入有误，请重新输入";
		}

		//年龄
		cout << "请输入年龄：" << endl;
		int age = 0;
		cin >> age;
		abs->personArray[ret].m_Age = age;

		//联系电话
		cout << "请输入联系电话：" << endl;
		string phone = "";
		cin >> phone;
		abs->personArray[ret].m_Phone = phone;

		//家庭住址
		cout << "请输入家庭住址：" << endl;
		string address;
		cin >> address;
		abs->personArray[ret].m_Addr = address;

		cout << "修改成功" << endl;
	}
	else
	{
		cout << "查无此人" << endl;
	}

	system("pause");
	system("cls");

}

//7.清空联系人
void cleanPerson(Addressbooks* abs)
{
	abs->m_Size = 0;
	cout << "通讯录已清空" << endl;
	system("pause");
	system("cls");
}

void showMenu()
{
	cout << "**************************" << endl;
	cout << "*****  1.添加联系人  *****" << endl;
	cout << "*****  2.显示联系人  *****" << endl;
	cout << "*****  3.删除联系人  *****" << endl;
	cout << "*****  4.查找联系人  *****" << endl;
	cout << "*****  5.修改联系人  *****" << endl;
	cout << "*****  6.清空联系人  *****" << endl;
	cout << "*****  0.退出通讯录  *****" << endl;
	cout << "**************************" << endl;
}

int main()
{
	Addressbooks abs;

	abs.m_Size = 0;

	int select = 0;

	while (true)
	{
		showMenu();

		cin >> select;
		switch (select)
		{
		case 1://1.添加联系人
			addPerson(&abs);
			break;
		case 2://2.显示联系人
			showPerson(&abs);
			break;
		case 3://3.删除联系人
			deletePerson(&abs);
			break;
		case 4://4.查找联系人
			findPerson(&abs);
			break;
		case 5://5.修改联系人
			modifyPerson(&abs);
			break;
		case 6://6.清空联系人
			cleanPerson(&abs);
			break;
		case 0://0.退出通讯录
			cout << "欢迎下次使用" << endl;
			system("pause");
			return 0;
			break;
		default:
			break;
		}
	}
	

	system("pause");
	return 0;
};
