import { useEffect, useState } from "react";
import { useForm } from "react-hook-form";
import { Link, useLocation, useNavigate } from "react-router";
import { toast } from "react-toastify";
import * as z from "zod";

import { zodResolver } from "@hookform/resolvers/zod";

import PageMeta from "../../components/common/PageMeta";
import Checkbox from "../../components/form/input/Checkbox";
import Input from "../../components/form/input/InputField";
import Label from "../../components/form/Label";
import Button from "../../components/ui/button/Button";
import { EyeCloseIcon, EyeIcon, Google, X } from "../../icons";
import { useLocalStorage } from "../../lib/LocalStorageProvider";
import { User } from "../../lib/types";
import { useLogin } from "../../services/auth";

const schema = z.object({
  email: z.string().email({ message: "Invalid email address." }).max(100, {
    message: "Email must be less than 100 characters."
  }),
  password: z.string().nonempty({ message: "Password is required." })
});

function LoginForm() {
  const location = useLocation();
  const navigate = useNavigate();
  const [, setUser] = useLocalStorage<User>("user", {
    uid: undefined,
    fname: undefined,
    lname: undefined,
    email: undefined,
    cid: undefined,
    rid: undefined,
    profile_picture_url: undefined
  });
  const login = useLogin(
    (response) => {
      localStorage.setItem("authToken", response.access_token);
      setUser({
        uid: response.uid,
        fname: response.fname,
        lname: response.lname,
        email: response.email,
        cid: response.cid,
        rid: response.rid,
        profile_picture_url: response.profile_picture_url
      });
      navigate(
        location.state?.from ? location.state.from.pathname : "/dashboard"
      );
    },
    (error) => {
      toast.error(error?.detail.message, { toastId: "login-error" });
    }
  );
  useEffect(() => {
    if (localStorage.getItem("authToken")) {
      navigate("/dashboard");
    }
    if (location.state?.toast === "unauthorized") {
      toast.error("Please login to continue.", { toastId: "unauthorized" });
    }
  }, [location.state?.toast, navigate]);
  const {
    register,
    handleSubmit,
    formState: { errors }
  } = useForm({
    resolver: zodResolver(schema),
    mode: "onChange"
  });
  const onSubmit = handleSubmit((data) => {
    login.mutate(data);
  });
  const [showPassword, setShowPassword] = useState(false);
  const [isChecked, setIsChecked] = useState(false);

  return (
    <form onSubmit={onSubmit}>
      <div className="space-y-6">
        <div>
          <Label htmlFor="email" required>
            Email
          </Label>
          <Input
            type="email"
            id="email"
            placeholder="name@example.com"
            {...register("email")}
            error={!!errors.email}
            hint={errors.email?.message}
          />
        </div>
        <div>
          <Label htmlFor="password" required>
            Password
          </Label>
          <div className="relative">
            <Input
              id="password"
              type={showPassword ? "text" : "password"}
              placeholder="Enter your password"
              {...register("password")}
              error={!!errors.password}
              hint={errors.password?.message}
            />
            <span
              onClick={() => setShowPassword(!showPassword)}
              className="absolute z-30 cursor-pointer right-4 top-3"
            >
              {showPassword ? (
                <EyeIcon className="fill-gray-500 dark:fill-gray-400 size-5" />
              ) : (
                <EyeCloseIcon className="fill-gray-500 dark:fill-gray-400 size-5" />
              )}
            </span>
          </div>
        </div>
        <div className="flex items-center justify-between">
          <div className="flex items-center">
            <Checkbox
              id="keep-logged-in"
              checked={isChecked}
              onChange={setIsChecked}
            />
            <label
              htmlFor="keep-logged-in"
              className="pl-3 font-normal text-gray-700 text-theme-sm dark:text-gray-400 cursor-pointer"
            >
              Keep me logged in
            </label>
          </div>
          <Link
            to="/forgot-password"
            className="text-sm text-brand-500 hover:text-brand-600 dark:text-brand-400"
          >
            Forgot password?
          </Link>
        </div>
        <div>
          <Button type="submit" className="w-full" size="sm">
            Log in
          </Button>
        </div>
      </div>
    </form>
  );
}

export default function Login() {
  return (
    <>
      <PageMeta title="Log In - AB Hire" description="Log in page" />
      <div className="flex flex-col justify-center flex-1 w-full max-w-md mx-auto pb-10">
        <div>
          <div className="mb-5 sm:mb-8">
            <h1 className="mb-2 font-semibold text-gray-800 text-title-sm dark:text-white/90 sm:text-title-md">
              Log In
            </h1>
            <p className="text-sm text-gray-500 dark:text-gray-400">
              Enter your email and password to log in!
            </p>
          </div>
          <div>
            <div className="grid grid-cols-1 gap-3 sm:grid-cols-2 sm:gap-5">
              <button className="inline-flex items-center justify-center gap-3 py-3 text-sm font-normal text-gray-700 transition-colors bg-gray-100 rounded-lg px-7 hover:bg-gray-200 hover:text-gray-800 dark:bg-white/5 dark:text-white/90 dark:hover:bg-white/10">
                <Google className="w-5 h-5" />
                Log in with Google
              </button>
              <button className="inline-flex items-center justify-center gap-3 py-3 text-sm font-normal text-gray-700 transition-colors bg-gray-100 rounded-lg px-7 hover:bg-gray-200 hover:text-gray-800 dark:bg-white/5 dark:text-white/90 dark:hover:bg-white/10">
                <X className="w-5 h-5 fill-current" />
                Log in with X
              </button>
            </div>
            <div className="relative py-3 sm:py-5">
              <div className="absolute inset-0 flex items-center">
                <div className="w-full border-t border-gray-200 dark:border-gray-800"></div>
              </div>
              <div className="relative flex justify-center text-sm">
                <span className="p-2 text-gray-400 bg-white dark:bg-gray-900 sm:px-5 sm:py-2">
                  Or
                </span>
              </div>
            </div>
            <LoginForm />
            <div className="mt-5">
              <p className="text-sm font-normal text-center text-gray-700 dark:text-gray-400 sm:text-start">
                Don&apos;t have an account? {""}
                <Link
                  to="/signup"
                  className="text-brand-500 hover:text-brand-600 dark:text-brand-400"
                >
                  Sign Up
                </Link>
              </p>
            </div>
          </div>
        </div>
      </div>
    </>
  );
}
