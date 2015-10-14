# GoogleFormSpammer
Spams Google Forms using Selenium. Harmless malicious toy. Uses 0 as phone number to undo.

Imports OpenQA.Selenium
Imports System.IO

Module Module1

    Sub Main()
        Dim url As String = "https://docs.google.com/forms/d/1ixeGBlblGRJ_OXXVSQlAF0InYGs3YQ122Igc491jDVA/viewform"
        Dim driver As New Firefox.FirefoxDriver

        Dim m_peFullName As By = By.Id("entry_590216545")
        Dim m_peSchool As By = By.Id("entry_304046455")

        Dim m_peClassA As By = By.Id("group_124822352_1")
        Dim m_peClassB As By = By.Id("group_124822352_2")
        Dim m_peClassC As By = By.Id("group_124822352_3")

        Dim m_peShirt1 As By = By.Id("group_191236689_1")
        Dim m_peShirt2 As By = By.Id("group_191236689_2")
        Dim m_peShirt3 As By = By.Id("group_191236689_3")
        Dim m_peShirt4 As By = By.Id("group_191236689_4")
        Dim m_peShirt5 As By = By.Id("group_191236689_5")

        Dim m_pePhone As By = By.Id("entry_1449937802")

        Dim m_peSubmit As By = By.Id("ss-submit")
        Dim m_peNew As By = By.ClassName("ss-bottom-link")

        Dim listClass As List(Of By) = New List(Of By)
        listClass.Add(m_peClassA)
        listClass.Add(m_peClassB)
        listClass.Add(m_peClassC)

        Dim listSize As List(Of By) = New List(Of By)
        listSize.Add(m_peShirt1)
        listSize.Add(m_peShirt2)
        listSize.Add(m_peShirt3)
        listSize.Add(m_peShirt4)
        listSize.Add(m_peShirt5)

        driver.Url = url

        Dim reader = File.OpenText("wpapoolwebrankingsWomen.txt")
        Dim line() As String
        While (reader.Peek() <> -1)
            line = reader.ReadLine().Split("	")

            'Console.WriteLine("Name=" & line(1))
            'Console.WriteLine("School=" & line(5).Split("(")(0))
            'Console.WriteLine("Number=" & line(0))

            'CInt(Math.Ceiling(Rnd() * n)) + 1

            driver.FindElement(m_peFullName).SendKeys(line(1))
            driver.FindElement(m_peSchool).SendKeys(line(5).Split("(")(0) & " Ranked " & line(0))

            driver.FindElement(listClass(CInt(Math.Ceiling(Rnd() * 3)) - 1)).Click()
            driver.FindElement(listSize(CInt(Math.Ceiling(Rnd() * 5)) - 1)).Click()

            driver.FindElement(m_pePhone).SendKeys("0")

            driver.FindElement(m_peSubmit).Click()
            driver.Manage.Timeouts.ImplicitlyWait(TimeSpan.FromSeconds(3))
            driver.FindElement(m_peNew).Click()
        End While

        Console.WriteLine("Finished")
        Console.Read()
    End Sub

End Module
