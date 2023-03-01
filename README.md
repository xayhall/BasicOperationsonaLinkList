# BasicOperationsonaLinkList
project for CSC228



#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

struct AirQuality
{
	string uniqueId;
	string indicatorId;
	string name;
	string measure;
	string measureInfo;
	string geoTypeName;
	string geoJoinId;
	string geoPlaceName;
	string timePeriod;
	string startDate;
	string dataValue;
	AirQuality *link;
};

AirQuality *head = nullptr;
AirQuality *current = nullptr;
AirQuality *newNode = nullptr;




void InitializeList()
{
	
	fstream file("BasicOperationsofaLinkList.txt");//opens the input file
	
	if (file.is_open())
	{
		while(file.good())
		{
			newNode = new AirQuality;
			getline(file, newNode->uniqueId);
			getline(file, newNode->indicatorId);
			getline(file, newNode->name);
			getline(file, newNode->measure);
			getline(file, newNode->measureInfo);
			getline(file, newNode->geoTypeName);
			getline(file, newNode->geoJoinId);
			getline(file, newNode->geoPlaceName);
			getline(file, newNode->timePeriod);
			getline(file, newNode->startDate);
			getline(file, newNode->dataValue);
			newNode->link = nullptr;
			
			if (head == nullptr)
			{
				head = newNode;
			}
			else
			{
				current = head;
				while(current->link != nullptr)
				{
					current = current->link;
				}
				current->link = newNode;
			}
	
		}
		file.close();
	}
	else 
		{
		cout << "An error has occured";
		}
}

void PrintList()
{
	current = head;
	
	while(current != nullptr)
	{
		
		if(current->uniqueId != "")
		{
		cout << "Unique Id: " << current->uniqueId << endl;
		cout << "Indicator Id: " << current->indicatorId << endl;
		cout << "Name: " << current->name << endl;
		cout << "Measure: " << current->measure << endl;
		cout << "Measure Info: " << current->measureInfo << endl;
		cout << "Geo Type Name: " << current->geoTypeName << endl;
		cout << "Geo Join Id: " << current->geoJoinId << endl;
		cout << "Geo Place Name: " << current->geoPlaceName << endl;
		cout << "Time Period: " << current->timePeriod << endl;
		cout << "Start Date: " << current->startDate << endl;
		cout << "Data Value: " << current->dataValue << endl;
		current = current->link;
		cout << endl;
		}
		else
		{
			break;
		}
	}	
}

int Length()
{
	int length = 0;
	
	current = head;
	
	while(current != nullptr)
	{
		
		if(current->uniqueId != "")
		{
			length++;
			current = current->link;
		}
		else
		{
			return length;
			break;
		}
	}	
	
}

int IsEmpty()
{
	current = head;
	
	if (current != nullptr)
	{
		return 0;
	}
	else
	{
		return -1;
	}
	
}

int main()
{
	//InitializeList();
	PrintList();
	cout <<Length() << endl;
	cout <<IsEmpty() << endl;
	cout << head;
	return 0;
}
