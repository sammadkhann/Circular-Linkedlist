# Circular-Linkedlist

Node.h

class Node
{
private:
	int data;
	Node* next;

public:
	Node();
	Node(int);
	void setData(int);
	void setNext(Node*);
	int getData();
	Node* getNext();
};


Linkedlist.h

#include"Node.h"

class Linklist

{
private:
	Node* head;
	Node* tail;
public:
	Linklist(); 
	bool isEmpty();
	void insertAtHead(int);
	void insertAtTail(int);
	void display();
	void insertAtTarget(int, int);
	Node* searchtarget(int);
	void removeNode(int);
};



Imp.cpp

#include"Linkedlist.h"
#include<iostream>

using namespace std;
//////////////////////////////////////////// Node Class ////////////////////////////////////////////

Node::Node()
{
	data = -1;
	next = NULL;


}
Node::Node(int data)
{
	this->data = data;
	next = NULL;


}
void Node::setData(int Data)
{
	this->data = data;
}
void Node::setNext(Node* next)
{
	this->next = next;
}

int Node::getData() {

	return data;
}

Node* Node::getNext() {

	return next;
}
//...........................Link list imp.......................................

Linklist::Linklist()
{
	head = NULL;
	tail = NULL;

}
bool Linklist::isEmpty()
{
	if (head == NULL)
	{
		return true;

	}
	else
	{
		return false;

	}

}
void Linklist::insertAtTail(int data)
{
	if (isEmpty())
	{ 
		Node* temp = new Node(data);
		head = temp;
		tail = temp;
		tail->setNext(head);
	}
	else
	{ 
		Node* temp = new Node(data);
		tail->setNext(temp);
		tail = temp;
		tail->setNext(head);
	}

}
void Linklist::insertAtHead(int data)
{
	if (isEmpty())
	{
		insertAtTail(data);
	}
	
	else
	{
		Node* temp = new Node(data);
		temp->setNext(head);
		head = temp;
		tail->setNext(head);

	}

}
void Linklist::display()
{

	if (isEmpty())
	{
		cout << "The linked list is empty." << endl;
		return ;
	}

	Node* temp = head;

	do
	{
		if (isEmpty())
		{
			cout << "list is empty :" << endl;
			return;
		}
		else
			cout << temp->getData() << "\t";
		temp = temp->getNext();
	} while (temp != head);

}
Node* Linklist::searchtarget(int toFind)
{
	Node* temp = head;
	do
	{
		if (temp->getData() == toFind)
		{
			return temp;

		}
		temp = temp->getNext();
	} while (temp != head);
	return NULL;
}
void Linklist::insertAtTarget(int target, int value)
{

	if (isEmpty())

	{
		cout << "List is empty" << endl;
		return;
	}
	else
	{
		Node* targetNode = searchtarget(target);
		if (targetNode == NULL)
		{
			cout << "Not found" << endl;
			return;
		}
		else
		{
			if (targetNode == tail)
			{
				insertAtTail(value);
			}
			else
			{
				Node* temp = new Node(value);
				temp->setNext(targetNode->getNext());
				targetNode->setNext(temp);
			}
		}
	}

}
void Linklist::removeNode(int toRemove)
{
	Node* targetNode = head;
	Node* prev = NULL;

	while (targetNode != NULL)
	{
		if (targetNode->getData() == toRemove)
		{
			break;
		}
		else
		{
			prev = targetNode;
			targetNode = targetNode->getNext();

		}
	}
	if (targetNode == NULL)
	{
		cout << "NOT found" << endl;
		return;
	}
	else
	{
		if (targetNode == head)
		{
			head = head->getNext();
			targetNode->setNext(NULL); 
			tail->setNext(head);
			delete targetNode;
		}
		else if (targetNode == tail)
		{
			tail = prev;
			tail->setNext(head);
			delete targetNode;

		}
		else
		{
			prev->setNext(targetNode->getNext());
			targetNode->setNext(NULL);
			delete targetNode;

		}
	}

}

Main.cpp

#include "Linkedlist.h"
#include <iostream>
#include <conio.h>
using namespace std;

int main()
{
	Node* ans = NULL;
	Linklist list1;
	list1.insertAtTail(10);
	list1.insertAtTail(15);
	list1.insertAtHead(5);
	list1.insertAtTail(7);
	list1.insertAtTail(19);
	list1.insertAtTail(20);
	list1.insertAtTail(25);
	list1.insertAtTail(30);
	list1.insertAtTail(16);

	list1.display();

	return 0;
}
