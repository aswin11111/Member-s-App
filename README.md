# Member-s-App
Final year project
from django.core.files.storage import FileSystemStorage
from django.http import HttpResponse
from django.shortcuts import render,redirect
import random,datetime

# Create your views here.
from members_app.models import house, login, house_member, committee, contact_book, achievements, imp_places, \
    committee_members, fund_information


def ward_add_achievements(request):
    return render(request,"Ward member/Addachivements8.html")

#achievement

def ward_add_achievements_post(request):

    achievementz=request.POST['textfield1']
    print('achievements')
    report = request.POST['textarea2']
    print('report')
    obj = achievements(achievements=achievementz,report=report,date=datetime.date.today())
    obj.save()
    return render(request, "Ward member/Addachivements8.html")


def ward_view_achievements(request):
    res = achievements.objects.all()
    return render(request,"Ward member/ViewAchievements.html",{'data':res})

def ward_edit_achievements(request,id):
    res=achievements.objects.get(pk=id)
    request.session['acpd']=id
    return render(request, "Ward member/editachievements.html",{'data': res})

def ward_edit_achievements_post(request):
    achievementz = request.POST['textfield1']
    report = request.POST['textarea2']
    acid=request.session['acpd']
    obj=achievements.objects.get(pk=acid)
    obj.achievements=achievementz
    obj.report=report
    obj.save()
    return redirect('/myapp/ward_view_achievements/')

def ward_view_achievements_search(request):
    if request.method=="POST":
        date1=request.POST['textfield']
        date2=request.POST['textfield2']
        comp_obj=achievements.objects.filter(date__gte=date1,date__lte=date2)
        return render(request, "Ward member/ViewAchievements.html", {'data': comp_obj})
    comp_obj=achievements.objects.all()
    return render(request,"Ward member/ViewAchievements.html",{'data':comp_obj})

def ward_del_view_achievements(request,id):
    res=achievements.objects.get(pk=id)
    res.delete()
    return redirect('/myapp/ward_view_achievements/')




def ward_add_committee(request):
    return render(request,"Ward member/Addcommittee3html.html")


#committee


def ward_add_committee_post(request):
    committee_name=request.POST['committeename']
    description=request.POST['description']
    obj = committee(committee_name=committee_name,description=description)
    obj.save()
    return ward_view_committee(request)
def ward_view_committee(request):
    res = committee.objects.all()
    return render(request,"Ward member/Viewcommittee.html",{'data':res})

def ward_edit_committee(request,id):
    res=committee.objects.get(pk=id)
    request.session['copd']=id
    return render(request, "Ward member/editcommittee.html",{'data': res})

def ward_edit_committee_post(request):
    committee_name=request.POST['committeename']
    description=request.POST['description']
    coid=request.session['copd']
    obj=committee.objects.get(pk=coid)
    obj.committee_name=committee_name
    obj.description=description
    obj.save()
    return redirect('/myapp/ward_view_committee/')


def ward_view_committee_search(request):
    if request.method == "POST":
        committee_name = request.POST['committee']
        print(committee_name)
        comp_obj = committee.objects.filter(committee_name__contains=committee_name)
        return render(request, "Ward member/Viewcommittee.html", {'data': comp_obj})
        comp_obj = committee.objects.all()
        return render(request, "Ward member/Viewcommittee.html", {'data': comp_obj})

def ward_del_view_committee(request,id):
    res=committee.objects.get(pk=id)
    res.delete()
    return redirect('/myapp/ward_view_committee/')


def ward_add_contactbook(request):
    return render(request,"Ward member/Addcontactbook18.html")

#Contact book

def ward_add_contactbook_post(request):
    contact_title = request.POST['textfield']

    contact_name = request.POST['textfield2']

    phone_number = request.POST['textfield3']

    obj = contact_book(contact_title=contact_title,contact_name=contact_name,phone_number=phone_number)
    obj.save()
    return render(request, "Ward member/Addcontactbook18.html")


def ward_view_contactbook(request):
    res = contact_book.objects.all()

    return render(request,"Ward member/viewcontactbook18.html",{'data':res})

def ward_edit_contactbook(request,id):
    res=contact_book.objects.get(pk=id)
    request.session['conpd']=id
    return render(request, "Ward member/editcontactbook.html",{'data': res})

def ward_edit_contactbook_post(request):
    contact_title = request.POST['textfield']

    contact_name = request.POST['textfield2']

    phone_number = request.POST['textfield3']
    conid=request.session['conpd']
    obj=contact_book.objects.get(pk=conid)
    obj.contact_title=contact_title
    obj.contact_name=contact_name
    obj.phone_number = phone_number
    obj.save()
    return redirect('/myapp/ward_view_contactbook/')

def ward_view_contactbook_search(request):
    if request.method == "POST":
        contact_title = request.POST['textfield']
        print(contact_title)
        comp_obj = contact_book.objects.filter(contact_title__contains=contact_title)
        return render(request, "Ward member/viewcontactbook18.html", {'data': comp_obj})
        comp_obj = contact_book.objects.all()
        return render(request, "Ward member/viewcontactbook18.html", {'data': comp_obj})

def ward_del_view_contactbook(request,id):
    res=contact_book.objects.get(pk=id)
    res.delete()
    return redirect('/myapp/ward_view_contactbook/')


def ward_add_edocument(request):
    return render(request,"Ward member/Addedocument10.html")

def ward_add_fundinformation(request):
    return render(request,"Ward member/Addfundinformation.html")

# fund information
def ward_add_fundinformation_post(request):

    information_title=request.POST['textfield3']
    print('information_title')
    description = request.POST['textarea']
    print('description')
    date = request.POST['textfield2']
    print('date')
    amount = request.POST['textfield']
    print('amount')
    obj = fund_information(information_title=information_title,description=description,date=date,amount=amount)
    obj.save()
    return render(request, "Ward member/Addfundinformation.html")

def ward_view_fundinformation(request):
    res =fund_information.objects.all()
    return render(request,"Ward member/viewfundinfo13.html",{'data':res})

def ward_edit_fundinformation(request,id):
    res=fund_information.objects.get(pk=id)
    request.session['fupd']=id
    return render(request, "Ward member/editfundinformation.html",{'data': res})

def ward_edit_fundinformation_post(request):
    information_title = request.POST['textfield3']
    description = request.POST['textarea']

    amount = request.POST['textfield']
    fuid=request.session['fupd']
    obj=fund_information.objects.get(pk=fuid)
    obj.information_title=information_title
    obj.description=description

    obj.amount=amount
    obj.save()
    return redirect('/myapp/ward_view_fundinformation/')

def ward_view_fundinformation_search(request):
    if request.method=="POST":
        date1=request.POST['textfield']
        date2=request.POST['textfield2']
        comp_obj=fund_information.objects.filter(date__gte=date1,date__lte=date2)
        return render(request, "Ward member/viewfundinfo13.html", {'data': comp_obj})
    comp_obj=fund_information.objects.all()
    return render(request,"Ward member/viewfundinfo13.html",{'data':comp_obj})

def ward_del_view_fundinformation(request,id):
    res=fund_information.objects.get(pk=id)
    res.delete()
    return redirect('/myapp/ward_view_fundinformation/')


#housemember

def ward_add_housemember(request):
    res=house.objects.all()
    return render(request,"Ward member/Addhousemember.html",{'data':res})

def ward_add_housemember_post(request):
    name=request.POST['name']
    email=request.POST['email']
    phonenumber = request.POST['phonenumber']
    bloodgroup = request.POST['bloodgroup']
    dob = request.POST['dob']
    hom=request.POST['hom']
    request.session['houid']=hom
    home=house.objects.get(pk=hom)
    image= request.FILES['fileField']
    fs=FileSystemStorage()
    sa=fs.save(image.name,image)
    url=fs.url(sa)
    pswrd=random.randint(0000,9999)
    res=login(username=email,password=pswrd,usertype="house_member")
    res.save()

    logg=login.objects.get(pk=res.pk)
    obj=house_member(name=name,email=email,phone=phonenumber,blood_group=bloodgroup,dob=dob,image=url,HOUSE=home,LOGIN=logg)
    obj.save()
    return ward_add_housemember(request)



def ward_view_house_member(request,houseid):
    hom=houseid
    homid=house.objects.get(pk=hom)
    res=house_member.objects.filter(HOUSE=homid)
    #resto=house_member.objects.all()
    return render(request,"Ward member/Viewhousemember.html",{'data':res})

def ward_del_housemember(request,id):
    res=house_member.objects.get(pk=id)
    res.delete()
    return redirect('myapp:ward_view_houses')

def ward_edit_housemembers(request,id):
    res=house_member.objects.get(pk=id)

    request.session['hmpd']=id
    return render(request, "Ward member/edithousemember.html",{'data': res})

def ward_edit_housemembers_post(request):
    name=request.POST['name']
    email=request.POST['email']
    phone = request.POST['phonenumber']
    blood_group = request.POST['bloodgroup']
    dob = request.POST['DOB']
    #image= request.POST['filefield']

    hmid=request.session['hmpd']
    obj=house.objects.get(pk=hmid)
    obj.name=name
    obj.email=email
    obj.phone=phone
    obj.blood_group=blood_group
    obj.dob=dob
    #obj.image=image
    obj.save()
    return redirect('myapp:ward_view_houses')




def ward_add_houses(request):
    return render(request,"Ward member/Addhouses2.html")

def ward_add_houses_post(request):
    house_name=request.POST['textfield']
    house_no=request.POST['textfield1']
    place = request.POST['textfield2']
    post = request.POST['textfield3']
    pin = request.POST['textfield4']
    landmark= request.POST['textfield5']
    category = request.POST['textfield6']
    obj=house(house_name=house_name,house_no=house_no,place=place,post=post,pin=pin,landmark=landmark,category=category)
    obj.save()
    return ward_view_houses(request)
def ward_view_houses(request):
    res=house.objects.all()
    return render(request,"Ward member/Viewhouses.html",{'data':res})

def ward_del_house(request,id):
    res=house.objects.get(pk=id)
    res.delete()
    return redirect('myapp:ward_view_houses')

def ward_edit_house(request,id):
    res=house.objects.get(pk=id)
    request.session['hupd']=id
    return render(request, "Ward member/edithouses.html",{'data': res})

def ward_edit_houses_post(request):
    house_name=request.POST['t1']
    house_no=request.POST['t2']
    place = request.POST['t3']
    post = request.POST['t4']
    pin = request.POST['t5']
    landmark= request.POST['t6']
    category = request.POST['t7']
    hid=request.session['hupd']
    obj=house.objects.get(pk=hid)
    obj.house_name=house_name
    obj.house_no=house_no
    obj.place=place
    obj.post=post
    obj.pin=pin
    obj.landmark=landmark
    obj.category=category
    obj.save()
    return redirect('myapp:ward_view_houses')


def ward_view_houses_search(request):
    if request.method == "POST":
        house_name = request.POST['searchhouse']
        print(house_name)
        comp_obj = house.objects.filter(house_name__contains=house_name)
        return render(request, "Ward member/Viewhouses.html", {'data': comp_obj})




def ward_add_impplaces(request):
    return render(request,"Ward member/Addimpplaces.html")

def ward_add_impplaces_post(request):
    name=request.POST['textfield1']
    print(name)
    longitude=request.POST['textfield2']
    print(longitude)
    latitude = request.POST['textfield3']
    print(latitude)
    obj=imp_places(name=name,longitude=longitude,latitude=latitude)
    obj.save()
    return ward_view_impplaces(request)

def ward_view_impplaces(request):
    res = imp_places.objects.all()
    return render(request,"Ward member/Viewimpplaces12.html",{'data': res})

def ward_edit_impplaces(request,id):
    res=imp_places.objects.get(pk=id)
    request.session['impd']=id
    return render(request, "Ward member/editimpplaces.html",{'data': res})

def ward_edit_impplaces_post(request):
    name = request.POST['textfield1']

    longitude = request.POST['textfield2']

    latitude = request.POST['textfield3']

    imid=request.session['impd']
    obj=imp_places.objects.get(pk=imid)
    obj.name=name
    obj.longitude=longitude

    obj.latitude=latitude
    obj.save()
    return redirect('/myapp/ward_view_impplaces/')

def ward_del_view_impplaces(request,id):
    res=imp_places.objects.get(pk=id)
    res.delete()
    return redirect('/myapp/ward_view_impplaces/')


def ward_add_notification(request):
    return render(request,"Ward member/Addnotification9.html")

def ward_add_polltopic(request):
    return render(request,"Ward member/Addpolltopic14.html")

def ward_add_work(request):
    return render(request,"Ward member/Addwork16.html")

def ward_login(request):
    return render(request,"Ward member/login.html")

#login

def ward_login_post(request):
    username=request.POST['uname']
    password=request.POST['pwd']
    try:
        res=login.objects.get(username=username,password=password)
        request.session["lid"]=res.pk
        # lid=request.session["lid"]
        if res.usertype=='wardmember':
            return ward_homepage(request)
        elif res.usertype=='commiteemember':
            return HttpResponse("commiteemember")
        else:
            return HttpResponse("invalid")

    except Exception as e:
        return e

    # return HttpResponse("yes")

# def ward_add_houses_post(request):
#     house_name=request.POST['textfield']
#     house_no=request.POST['textfield1']
#     place = request.POST['textfield2']
#     post = request.POST['textfield3']
#     pin = request.POST['textfield4']
#     landmark= request.POST['textfield5']
#     category = request.POST['textfield6']
#     return HttpResponse("yes")
#

def ward_meetings(request):
    return render(request,"Ward member/meetings5.html")

def ward_memberrequest(request):
    comp_obj = committee_members.objects.filter(approve_status="pending")

    return render(request,"Ward member/memberrequest4.html",{'data': comp_obj})

def ward_searchbloodgroup(request):
    return render(request,"Ward member/Searchbloodgroup7.html")

def ward_sendreply(request):
    return render(request,"Ward member/sendreply6.html")



def ward_view_committeemember(request):
    return render(request,"Ward member/Viewcommitteemember.html")

def ward_view_complaint(request):
    return render(request,"Ward member/Viewcomplaint6.html")


def ward_view_edocument(request):
    return render(request,"Ward member/viewedocument10.html")

def ward_view_meeting(request):
    return render(request,"Ward member/Viewmeeting5.html")

def ward_view_needrequest(request):
    return render(request,"Ward member/viewneedrequest11.html")

def ward_view_notification(request):
    return render(request,"Ward member/Viewnotification9.html")

def ward_view_pollstatus(request):
    return render(request,"Ward member/viewpollstatus.html")

def ward_view_polltopic(request):
    return render(request,"Ward member/viewpolltopic15.html")

def ward_view_workstatus(request):
    return render(request,"Ward member/viewworkstatus17.html")

def ward_homepage(request):
    return render(request,"index.html")




def ward_edit_edocument(request):
    return render(request,"Ward member/editedocument.html")





def ward_edit_meetings(request):
    return render(request,"Ward member/editmeetings.html")

def ward_edit_notification(request):
    return render(request,"Ward member/editnotification.html")




